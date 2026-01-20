## Leverage the SDK

### Use case: Hardware-in-the-Loop (HITL) testing. Only for rootfs.

**Goal:** speed up development and testing by avoiding full image rebuilds and reflashing the target for every code/config change.

**Idea:** A single Yocto build produces:
- a **target image** (runs on QEMU/real device)
- a **host SDK** (used on the server/host machine)

The SDK provides a consistent host environment and can also ship host-side tooling (via `nativesdk-*` packages), such as NFS-Ganesha and our HITL helper scripts.

---

### Workflow

1) **Boot the target**
- Flash/boot the Yocto image on the target (or start the QEMU image).
- Ensure the target has NFS client support (e.g., `nfs-utils`) and network connectivity to the host.

2) **Prepare the host with the SDK**
- Install the Yocto SDK on the host machine.
- Source the environment script:
  ```bash
  source /opt/<sdk-path>/environment-setup-*
