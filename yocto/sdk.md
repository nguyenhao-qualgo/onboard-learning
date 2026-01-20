# Generate SDK

https://docs.yoctoproject.org/sdk-manual/using.html

## What is the SDK and why do we need it?

The Yocto SDK provides a ready-to-use development environment for building applications that will run on the target image. Instead of manually installing cross-compilers and matching target libraries on your host machine, the SDK guarantees that everyone builds against the same toolchain and the same target ABI.

Benefits:
- **Reproducible builds** across developers and CI
- **Binary compatibility** with the target (same libc, compiler, and library versions)
- **Fast onboarding** (install SDK + source one script)

---

## What the SDK includes

### 1) Cross toolchain (host → target)
- Cross compiler (e.g., `aarch64-poky-linux-gcc/g++`)
- Linker, assembler, binutils
- Common debug tools (e.g., `gdb`, `objdump`, `readelf`)

### 2) Target sysroot
A filesystem tree containing the **headers and libraries from the target** required to compile and link applications correctly, for example:
- C/C++ headers and runtime libraries
- Common libraries (e.g., OpenSSL, zlib, libcurl, systemd libs — depending on your image)
- `pkg-config` metadata (`*.pc` files) so build systems can discover include/lib paths

> Think of the sysroot as “what the target has available for linking”, packaged for the host build environment.

### 3) Environment setup script
The SDK provides an environment script (typically named `environment-setup-*`) that configures:
- `CC`, `CXX`, `AR`, `LD`, `STRIP`
- `PKG_CONFIG_PATH`, `PKG_CONFIG_SYSROOT_DIR`
- `CFLAGS`, `LDFLAGS`
- Target triplet and sysroot paths

After sourcing this script, standard build systems (CMake, Meson, Autotools, Make) can cross-compile with minimal changes.

### 4) Optional host-side tools (nativesdk packages)
You can also include host utilities inside the SDK (built for the host OS but managed by Yocto), such as:
- custom development helpers
- host-run services/tools used in workflows (e.g., NFS-Ganesha for HITL)

This is controlled via `TOOLCHAIN_HOST_TASK`.

---

## SDK types in Yocto

- **Standard SDK** (`populate_sdk`): fixed SDK generated from the build (most common)
- **Extensible SDK (eSDK)** (`populate_sdk_ext`): supports extending the SDK after installation (more flexible, larger)

For most application development workflows, the standard SDK is enough.

---
