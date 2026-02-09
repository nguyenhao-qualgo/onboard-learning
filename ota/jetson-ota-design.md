# Jetson Orin Drone OTA Design

## GCS-mediated OTA with Error Codes — FULL DESIGN (Overview + Flows 1→6)

---

## Global Overview

This document defines a **production-grade OTA (Over-The-Air Update)** architecture for **Jetson Orin–based drones**, designed with safety, security, and fleet-scale operability in mind.

### Core Principles

* **Safety-first**

  * No install or reboot while airborne
  * Flight Controller (FC) is the final safety authority
* **Authority separation**

  * GCS decides *what / when / who* to update
  * Jetson OTA Agent executes update steps
  * FC enforces flight and reboot safety
* **Atomicity**

  * A/B rootfs with automatic rollback
* **Security**

  * Offline-signed manifests and artifacts
  * Device authentication via mTLS
  * Anti-rollback protection
* **Observability**

  * Deterministic OTA states
  * Machine-readable error codes
  * Idempotent status reporting

All diagrams use **Mermaid-compatible syntax** and can be reviewed directly in **VS Code**.

---

## 1) Error Code Model

### Purpose

* Machine-readable failure handling
* Fleet-level automation (retry, defer, quarantine, rollback)
* Safety / FMEA traceability

### Rules

* Format: `DOMAIN_XXXX`
* Always report `{state, error_code}`
* One dominant error per failure path

### Core Error Code Set (excerpt)

| Domain | Error Code | Meaning                             |
| ------ | ---------- | ----------------------------------- |
| GATE   | GATE_0001  | Vehicle armed                       |
| GATE   | GATE_0002  | Not landed                          |
| GATE   | GATE_0003  | Battery below threshold             |
| NET    | NET_0005   | HTTP Range / resume unsupported     |
| DL     | DL_0101    | Chunk hash mismatch                 |
| SEC    | SEC_0201   | Manifest signature invalid          |
| SEC    | SEC_0202   | Certificate chain invalid / expired |
| SEC    | SEC_0203   | Artifact hash mismatch              |
| SEC    | SEC_0204   | Anti-rollback violation             |
| COMP   | COMP_0250  | Incompatible hardware / software    |
| INST   | INST_0301  | Write inactive slot failed          |
| INST   | INST_0302  | Post-write verification failed      |
| INST   | INST_0303  | Insufficient storage                |
| BOOT   | BOOT_0401  | Failed to set boot flags            |
| HLTH   | HLTH_0503  | Flight controller handshake failed  |
| MCAG   | MCAG_0601  | OTA-Agent service unavailable       |
| MCAG   | MCAG_0602  | OTA-Agent internal error            |

---

## 2) System Architecture — Block Diagram

```mermaid
flowchart LR
  subgraph Cloud["Cloud (Optional)"]
    OTA["OTA Backend"]
    SIGN["Signing Service (Offline / HSM)"]
    MON["Monitoring"]
  end

  subgraph GCS["Ground Control Station"]
    GCSAG["OTA Orchestrator"]
    CACHE["Artifact Cache / Proxy"]
  end

  subgraph Drone["Drone (Jetson Orin)"]
    AG["OTA Agent"]
    FC["Flight Controller"]
    BOOT["A/B Boot Control"]
    SLOTS[("Slot A / Slot B")]
  end

  SIGN --> OTA
  OTA --> MON
  OTA --> GCSAG
  GCSAG --> CACHE
  GCSAG <-->|mTLS| AG
  AG <-->|MAVLink / IPC| FC
  AG --> BOOT --> SLOTS
```

### Explanation

* Signing Service signs all OTA manifests and artifacts.
* OTA Backend stores artifacts and rollout metadata (optional).
* GCS OTA Orchestrator is the OTA authority and controls rollout decisions.
* Jetson OTA Agent executes OTA operations but does not decide rollout policy.
* Flight Controller enforces safety gating (e.g. armed / in-flight checks).
* A/B Boot Chain guarantees atomic updates and automatic rollback.

### Notes

* **Control-plane**: manifest, policy, status (GCS ↔ Agent)
* **Data-plane**: artifact download (via GCS cache or Cloud/CDN)
* Proxy / MC service handles authentication, rate limiting, and auditing but **never modifies artifacts or manifests**.

## 3) System overview Phase Map

```mermaid
graph TD
  %% Style Definitions
  classDef gcs fill:#f5f5f5,stroke:#9e9e9e,color:#333;
  classDef agent fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#01579b;
  classDef bootloader fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#e65100;
  classDef danger fill:#ffebee,stroke:#c62828,color:#c62828;

  %% EXTERNAL - GCS SIDE
  GCS([GCS])

  %% MC SIDE (Jetson Board)
  subgraph MC [Jetson]
    direction TB

    subgraph Stage1 [Phase 1: OTA Agent Preparation]
      direction TB
      Check[Check Drone Safety:<br/>Landed/Disarmed]
      DL[Download & Hash Verify Artifacts]
    end

    subgraph Stage2 [Phase 2: OTA Agent Installation]
      direction TB
      Write[Write to Inactive Slot]
      Config[Set Bootloader: Priority + Retry=3]
    end

    subgraph Stage3 [Phase 3: Bootloader Check]
      direction TB
      SigCheck{Try to boot?}
      RetryCheck{Retries Remaining?}
      OSBoot[Start OS]
      HardRollback[HARD ROLLBACK: Switch Back to Good Slot]
    end

    subgraph Stage4 [Phase 4: OTA Agent Check]
      direction TB
      Health[Health Check: Handshake with Flight Controller, ...]
      Commit[Mark Slot Good Permanently]
      SoftRollback[SOFT ROLLBACK: Mark Slot Bad & Reboot]
    end
  end

  %% --- CONNECTIONS (Fixed to avoid Lexical Errors) ---
  GCS -- "Sends Update Message" --> Check

  %% Phase 1
  Check --> DL

  %% Phase 2
  DL --> Write
  Write --> Config

  %% Phase 3
  Config -- "Reboot Trigger" --> SigCheck
  SigCheck --> OSBoot
  SigCheck -.-> RetryCheck
  RetryCheck -.-> SigCheck
  RetryCheck  -.-> HardRollback

  %% Phase 4
  OSBoot --> Health
  Health --> Commit
  Health  -.-> SoftRollback
  SoftRollback -.-> HardRollback

  %% Final Outcomes
  HardRollback -.-> Success([System Restored to Old Version])
  Commit --> Success([Update Complete & Active])

	%% Legend Construction (Floating)
  LegendBox[───▶ Normal Flow<br/>-------▶ Error Flow]

  %% Applying classes
  class GCS gcs;
  class Check,DL,Write,Config,Health,Commit,SoftRollback agent;
  class SigCheck,RetryCheck,HardRollback,OSBoot bootloader;
  class HardRollback,SoftRollback danger;
```

---

## 4) OTA-Agent state machine

```mermaid
graph TD
  %% Style Definitions
  classDef success stroke:#2e7d32,stroke-width:2px,fill:#e8f5e9,color:#1b5e20;
  classDef failure stroke:#c62828,stroke-width:2px,fill:#ffebee,color:#b71c1c;
  classDef neutral stroke:#333,stroke-width:2px,fill:#f5f5f5;
  classDef legend fill:#ffffff,stroke:#999,stroke-dasharray: 5 5;

  %% State Nodes
  IDLE((IDLE))
  DOWNLOAD(DOWNLOAD)
  INSTALL(INSTALL)
  REBOOT(REBOOT)
  COMMIT(COMMIT)
  FAILURE{{FAILURE}}
  ROLLBACK{{ROLLBACK}}

  %% Normal Success Flow
  IDLE --> DOWNLOAD
  DOWNLOAD --> INSTALL
  INSTALL --> REBOOT
  REBOOT --> COMMIT
  COMMIT --> IDLE

  %% Error & Rollback Flows
  DOWNLOAD -.-> IDLE
  INSTALL -.-> FAILURE
  COMMIT -.-> FAILURE
  FAILURE -.-> IDLE

  %% The Bootloader / Agent Safety Net
  REBOOT -.-> ROLLBACK
  ROLLBACK -.-> FAILURE

  %% Legend Construction (Floating)
  LegendBox[───▶ Normal Flow<br/>-------▶ Error Flow]

  %% Link classes
  class IDLE,DOWNLOAD,INSTALL,COMMIT neutral;
  class REBOOT success;
  class ROLLBACK,FAILURE failure;
  class LegendBox legend;
```

### Explanation

This diagram represents the end-to-end OTA state flow executed by the Jetson OTA Agent, from idle to completion. It is designed to be deterministic, restart-safe, and auditable.

Key characteristics:

* The OTA Agent always starts and ends in the IDLE state.
* All safety checks occur before any irreversible action (install or reboot).
* Download and verification are separated from installation.
* Reboot is explicitly gated by the Flight Controller.
* Health validation decides commit vs rollback automatically.

State descriptions:

* IDLE: State where no communication with GCS nor is there any update in progress
* DOWNLOAD: There is an update available for device and try to download.
* INSTALL: Writes update to the inactive A/B slot only.
* REBOOT: System prepared for reboot, waiting for final safety approval.
* COMMIT: Device is up and running after rebooting, commit makes the update persistent
* FAILURE: Reports Failure to GCS, clean up and recovery.
* ROLLBACK: If the new update is broken and need to go back the previous one.

Any failure in the workflow results in a safe return to IDLE, either immediately or after rollback.

---

## 5) Sequence — Check + Decide + Download

```mermaid
sequenceDiagram
  autonumber
  participant FC as Flight Controller
  participant GCS as GCS OTA Orchestrator
  participant AG as Jetson OTA Agent

  GCS->>AG: Query device info

  alt MCAG_0601 / MCAG_0602
    AG-->>GCS: status(error_code=MCAG_060x)
  else OK
    AG->>FC: Query vehicle state
    FC-->>AG: landed, armed, battery, mission
    AG-->>GCS: version, model, vehicle_state
  end

  GCS->>GCS: Evaluate rollout policy
  alt Not eligible / up-to-date
    GCS-->>AG: No update
  else Update available
    GCS-->>AG: Update available
  end

  AG->>AG: Pre-download gating
  alt gating fail
    AG-->>GCS: status(GATE_000x)
  else gating pass
    AG->>GCS: GET manifest
    GCS-->>AG: manifest

    AG->>AG: Compatibility + anti-rollback check
    alt incompatible
      AG-->>GCS: status(COMP_0250)
    else compatible
      AG->>AG: Init downloader
      AG->>GCS: GET artifact (HTTP Range)
      loop per chunk
        AG->>AG: Receive + hash verify
      end

      AG->>AG: Verify signature / hashes / rollback index
      alt verify fail
        AG-->>GCS: status(SEC_020x)
      else verify ok
        AG-->>GCS: status(VERIFY_OK)
      end
    end
  end
```

### Explanation

This phase determines **whether an update should happen** and **safely prepares artifacts** without modifying the running system.

* GCS queries the OTA Agent to obtain software version, model, and vehicle state.
* The OTA Agent queries the Flight Controller (FC) to confirm flight safety signals (armed, landed, battery, mission state).
* GCS evaluates rollout policy (version targeting, phased rollout, blacklists).
* Pre-download gating ensures downloads only happen under acceptable ground conditions.
* The manifest defines compatibility, hashes, rollback index, and signatures.
* Artifacts are downloaded using resumable HTTP Range requests.
* Integrity is verified at chunk-level and full-artifact level.
* No persistent system changes occur in this phase; failures always return to IDLE.

This design allows **safe retries, bandwidth control, and offline preparation** before installation.

---

## 6) Sequence — Install to Inactive Slot (A/B)

```mermaid
sequenceDiagram
  autonumber
  participant AG as Jetson OTA Agent
  participant BC as Boot Control
  participant GCS as GCS

  AG->>AG: Acquire OTA lock
  AG->>AG: Select inactive slot
  AG->>AG: Validate storage

  alt insufficient storage
    AG-->>GCS: status(INST_0303)
  else storage ok
    AG->>AG: Write image to inactive slot
    AG->>AG: Post-write verification
    alt write/verify fail
      AG-->>GCS: status(INST_0301 / INST_0302)
    else success
      AG->>BC: Set next boot slot + reset attempt counter
      alt boot flag fail
        AG-->>GCS: status(BOOT_0401)
      else success
        AG-->>GCS: status(INSTALLED_INACTIVE_SLOT)
      end
    end
  end
```

### Explanation

This phase performs the **atomic installation** of the new software while protecting the currently running system.

* A single-writer lock prevents concurrent OTA attempts.
* The OTA Agent selects the inactive rootfs slot.
* Storage capacity and filesystem integrity are validated before writing.
* The new image is written only to the inactive slot.
* A post-write verification step confirms data integrity.
* Boot flags are updated *only after* a successful write and verification.
* The active slot remains untouched at all times.

If any failure occurs, the device remains bootable on the previous slot, guaranteeing **non-bricking behavior**.

---

## 7) Sequence — Reboot + Health + Rollback

```mermaid
sequenceDiagram
  autonumber
  participant FC as Flight Controller
  participant AG as Jetson OTA Agent
  participant GCS as GCS

  AG->>FC: Pre-reboot safety check
  FC-->>AG: safe / unsafe

  alt unsafe
    AG-->>GCS: status(GATE_000x, deferred=true)
  else safe
    AG-->>GCS: status(OK)
    AG->>AG: Reboot into new slot

    Note over AG,GCS: Device reboot

    AG->>AG: Boot-level health checks
    AG->>FC: FC handshake
    FC-->>AG: OK / FAIL

    alt health fail
      AG-->>GCS: status(HLTH_050x)
      AG->>AG: Mark slot bad + rollback
      AG->>AG: Reboot
    else health pass
      AG->>AG: Commit new slot
      AG-->>GCS: status(OK)
    end
  end
```

### Explanation

This phase transitions execution to the new slot and validates system correctness before committing the update.

* A final safety check with the Flight Controller ensures reboot is allowed.
* Reboots are deferred if the vehicle is armed, airborne, or unsafe.
* After reboot, the OTA Agent performs layered health checks:

  * OS and critical service availability
  * Application and middleware health
  * FC handshake and telemetry sanity
* On any failure, the new slot is marked bad and an automatic rollback occurs.
* Commit only happens after all checks pass.

This guarantees **fail-safe behavior**, even across power loss or partial updates.

---

## Final Guarantees

* No OTA install or reboot while airborne
* Cryptographically verified artifacts
* Automatic rollback on any failure
* GCS-controlled rollout policy
* Deterministic, auditable OTA state machine

---

## There are 3 critical steps in OTA
- [1. Sequence — Check + Decide + Download](#5-sequence--check--decide--download)
- [2. Sequence — Install to Inactive Slot (A/B)](#6-sequence--install-to-inactive-slot-ab)
- [3. Sequence — Reboot + Health + Rollback](#7-sequence--reboot--health--rollback)


## Q&A
1) When introducing an *OTA-Agent* service, how should it communicate with the *GCS*? Should all *GCS* interactions be routed through an existing proxy MC service?

---

