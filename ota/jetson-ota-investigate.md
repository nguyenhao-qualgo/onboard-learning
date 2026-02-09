# Investigate OTA Updates on NVIDIA Jetson Orin Nano (NVIDIA L4T vs Yocto/meta-tegra)

## Goal
Evaluate OTA update mechanisms for Jetson Orin Nano and decide what artifacts we actually need in our Yocto-based system.

## References
- NVIDIA: *Preparing the OTA Payload Package*  
  https://docs.nvidia.com/jetson/archives/r36.4.4/DeveloperGuide/SD/SoftwarePackagesAndTheUpdateMechanism.html#preparing-the-ota-payload-package
- NVIDIA: *Update and Redundancy → Manually trigger the capsule update*  
  https://docs.nvidia.com/jetson/archives/r36.4.4/DeveloperGuide/SD/Bootloader/UpdateAndRedundancy.html#manually-trigger-the-capsule-update


---

## 1) Traditional NVIDIA OTA (L4T mechanism)

### What NVIDIA OTA package typically includes
NVIDIA scripts can produce an OTA package containing multiple artifacts:

1) **rootfs image**  
   - A compressed root filesystem image written to the **rootfs A/B** partitions.

2) **BUP (Bootloader Update Payload)**  
   - Bootloader capsule payload used to update **bootloader A/B**.

3) **boot.img**  
   - Written directly into the **A/B_kernel** partition.  
   - **Usage:** see [Boot modes and the role of `boot.img`](#boot-modes-and-the-role-of-bootimg)

4) **kernel-dtb**  
   - Written directly into the **A/B_kernel-dtb** partition.  
   - **Usage:** see [Boot modes and the role of `boot.img`](#boot-modes-and-the-role-of-bootimg)

5) **ESP (EFI System Partition) contents**  
   - Contains UEFI applications such as `bootaa64.efi`.

### Boot modes and the role of `boot.img`
NVIDIA supports multiple boot modes, including:
- **L4T Launcher** (default)
- **boot.img partition** mode

The mode can be controlled via the UEFI variable `L4TDefaultBootMode`:
- `0x00` - Boot via GRUB
- `0x01` - Boot via extlinux in an ext4 filesystem
- `0x02` - Boot via `boot.img` partition
- `0x03` - Boot recovery image
- `0xFF` - Default behavior

> **Note:** If our platform boots through a custom EFI application (e.g., `secondLoader`) that loads `Image` and `initrd` from rootfs, then `boot.img`/`kernel-dtb` may not be required.

---

## 2) Yocto / meta-tegra approach (OTA “Yocto side”)

### Key observation
Yocto already produces most of the needed update artifacts:
- **rootfs**: Yocto can output many formats (`ext4`, `tar.gz`, `ext4.gz`, …). We can pick one suitable for our update strategy.
- **ESP output**: `meta-tegra` can produce the ESP partition image/content (re-usable).
- **BUP equivalent**: `meta-tegra` generates the bootloader capsule as `TEGRA_BL.Cap`.

### Likely not needed (for our design)
`boot.img` and `kernel-dtb` may be unnecessary because our EFI application (`secondLoader`) boots using `Image` and `initrd` inside rootfs to validate secure boot and continue boot.

---

## Partition layout (current assumptions)
- **rootfs A/B**
  - Default devices: `/dev/nvme0n1p1` and `/dev/nvme0n1p2`

- **ESP**
  - Default device: `/dev/nvme0n1p11`
  - Auto-mounted at: `/boot/efi`

### BUP / capsule placement requirement
To stage the bootloader capsule update:
- Ensure **ESP is mounted**
- Copy `TEGRA_BL.Cap` to:
  - `/boot/efi/EFI/UpdateCapsule/TEGRA_BL.Cap`

---

## Triggering BUP (capsule) update

### Option A — manually set `OsIndications` bit2
```bash
cd /sys/firmware/efi/efivars/
printf "\x07\x00\x00\x00\x04\x00\x00\x00\x00\x00\x00\x00" > /tmp/var_tmp.bin
dd if=/tmp/var_tmp.bin of=OsIndications-8be4df61-93ca-11d2-aa0d-00e098032b8c bs=12
sync
```

### Option B — use existing helper script
`/usr/bin/oe4t-set-uefi-OSIndications`


## 3) Investigate Rollback machenism
### EFI Variables

- **BootChainOsCurrent**  
  Indicates the currently active boot slot.

- **RootfsStatusSlotA/B**  
  Boot status counter used to determine system health of its slot.

### Boot Slot Management and Rollback

These EFI variables can be used to implement an active boot slot selection and rollback mechanism.

#### Root Filesystem Status

- `RootfsStatusSlotA/B = 0` → **Bad** (boot failed or system unhealthy)
- `RootfsStatusSlotA/B > 0` → **Good** (boot successful)

#### Boot Slot Mapping

- `BootChainOsCurrent = 0` → **Slot A**
- `BootChainOsCurrent = 1` → **Slot B**

#### TODO: Continuing adding more informations