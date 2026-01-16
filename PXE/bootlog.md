```bash
>>Start PXE over IPv4.
  Station IP address is 192.168.42.118

  Server IP address is 192.168.42.1
  NBP filename is bootaa64.efi
  NBP filesize is 878872 Bytes
 Downloading NBP file...

  NBP file downloaded successfully.
[uefi1] UefiMain() start. Loading encrypted \EFI\BOOT\secondLoader.enc via MemMa
p DP
[uefi1] No SimpleFileSystem (PXE boot). Downloading via PXE TFTP...
[pxelib] PXE downloaded 'secondLoader.enc' size=35124 bytes
[uefi1] PXE loaded encrypted file: EncBuffer=0x266BB5018 EncSize=35124
[uefi1] Loaded encrypted \EFI\BOOT\secondLoader.enc at 0x266BB5018, size 35124 b
ytes
[uefi1] DecryptUefi2: decrypted 35096 bytes using BaseCryptLib AES-256-GCM
[uefi1] Set uefi2 LoadOptions: BOOT=PXE
[uefi1] LoadImage(uefi2) OK, starting...
[uefi2] UefiMain() start
[uefi2] Current BOOT_FW_VARIABLE_NAME: 1
[uefi2] Current BOOT_OS_VARIABLE_NAME: 1
[uefi2] PXE detected -> load kernel/initrd from PXE
[uefi2] LoadAndStartKernelFromPxe() entered
[pxelib] PXE downloaded 'Image' size=42177304 bytes
[pxelib] PXE downloaded 'initrd' size=8244988 bytes
[uefi2] Kernel downloaded at 0x26477C018, size 42177304 bytes
[uefi2] Initrd downloaded at 0x263F9F018, size 8244988 bytes
[pxelib] PXE downloaded 'cmdline.txt' size=159 bytes
[uefi2] Using cmdline from TFTP: root=/dev/nfs nfsroot=192.168.42.1:/volume1/nfs
_root/ nfsopts=vers=3,tcp,nolock ip=dhcp net.ifnames=0 console=ttyTCU0,115200 fi
rmware_class.path=/etc/firmware
[uefi2] Starting kernel (PXE)...
EFI stub: Booting Linux Kernel...
EFI stub: UEFI Secure Boot is enabled.
EFI stub: Using DTB from configuration table
EFI stub: Loaded initrd from LINUX_EFI_INITRD_MEDIA_GUID device path
EFI stub: Exiting boot services...
EFI stub: UEFI Secure Boot is enabled.
��debugfs initialized
��I/TC: Reserved shared memory is disabled
I/TC: Dynamic shared memory is enabled
I/TC: Normal World virtualization support is disabled
I/TC: Asynchronous notifications are disabled
��[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x410fd421]
[    0.000000] Linux version 5.15.148-l4t-r36.4.4-1012.12+gc8a82765359e (oe-user@oe-host) (aarch64-oe4t-linux-gcc (GCC) 13.4.0, GNU ld (GNU Binutils) 2.42.0.20240723) #1 SMP PREEMPT Tue Jul 1 10:48:42 UTC 2025 ()
[    0.000000] Machine model: NVIDIA Jetson Orin Nano Engineering Reference Developer Kit Super
[    0.000000] efi: EFI v2.70 by EDK II
[    0.000000] efi: RTPROP=0x26d82f198 SMBIOS=0xffff0000 SMBIOS 3.0=0x26d200000 MEMATTR=0x26711b018 ESRT=0x26711c398 RNG=0x25b170018 MEMRESERVE=0x25b960f18 
[    0.000000] random: crng init done
[    0.000000] secureboot: Secure boot enabled
[    0.000000] esrt: Reserving ESRT space from 0x000000026711c398 to 0x000000026711c3d0.
[    0.000000] Reserved memory: created CMA memory pool at 0x000000024a000000, size 256 MiB
[    0.000000] OF: reserved mem: initialized node linux,cma, compatible id shared-dma-pool
[    0.000000] NUMA: No NUMA configuration found
[    0.000000] NUMA: Faking a node at [mem 0x0000000080000000-0x0000000277ffffff]
[    0.000000] NUMA: NODE_DATA [mem 0x271308800-0x27130afff]
[    0.000000] Zone ranges:
[    0.000000]   DMA      [mem 0x0000000080000000-0x00000000ffffffff]
[    0.000000]   DMA32    empty
[    0.000000]   Normal   [mem 0x0000000100000000-0x0000000277ffffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000080000000-0x00000000bdffffff]
[    0.000000]   node   0: [mem 0x00000000c2000000-0x00000000fffdffff]
[    0.000000]   node   0: [mem 0x00000000fffe0000-0x00000000ffffffff]
[    0.000000]   node   0: [mem 0x0000000100000000-0x000000025e249fff]
[    0.000000]   node   0: [mem 0x000000025e24a000-0x000000025e40bfff]
[    0.000000]   node   0: [mem 0x000000025e40c000-0x000000026b8effff]
[    0.000000]   node   0: [mem 0x000000026b8f0000-0x000000026d82ffff]
[    0.000000]   node   0: [mem 0x000000026d830000-0x0000000271dfffff]
[    0.000000]   node   0: [mem 0x0000000271e00000-0x0000000271ffffff]
[    0.000000]   node   0: [mem 0x0000000272000000-0x000000027259ffff]
[    0.000000]   node   0: [mem 0x0000000272f00000-0x0000000272ffffff]
[    0.000000]   node   0: [mem 0x0000000276000000-0x0000000277ffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000080000000-0x0000000277ffffff]
[    0.000000] On node 0, zone DMA: 16384 pages in unavailable ranges
[    0.000000] On node 0, zone Normal: 2400 pages in unavailable ranges
[    0.000000] On node 0, zone Normal: 12288 pages in unavailable ranges
[    0.000000] psci: probing for conduit method from DT.
[    0.000000] psci: PSCIv1.1 detected in firmware.
[    0.000000] psci: Using standard PSCI v0.2 function IDs
[    0.000000] psci: Trusted OS migration not required
[    0.000000] psci: SMC Calling Convention v1.2
[    0.000000] percpu: Embedded 29 pages/cpu s79512 r8192 d31080 u118784
[    0.000000] Detected PIPT I-cache on CPU0
[    0.000000] CPU features: detected: Address authentication (architected algorithm)
[    0.000000] CPU features: detected: GIC system register CPU interface
[    0.000000] CPU features: detected: Virtualization Host Extensions
[    0.000000] CPU features: detected: Hardware dirty bit management
[    0.000000] CPU features: detected: Spectre-v4
[    0.000000] CPU features: detected: Spectre-BHB
[    0.000000] CPU features: kernel page table isolation forced ON by KASLR
[    0.000000] CPU features: detected: Kernel page table isolation (KPTI)
[    0.000000] alternatives: patching kernel code
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 2001056
[    0.000000] Policy zone: Normal
[    0.000000] Kernel command line: root=/dev/nfs nfsroot=192.168.42.1:/volume1/nfs_root/ nfsopts=vers=3,tcp,nolock ip=dhcp net.ifnames=0 console=ttyTCU0,115200 firmware_class.path=/etc/firmware
[    0.000000] Unknown kernel command line parameters "nfsopts=vers=3,tcp,nolock", will be passed to user space.
[    0.000000] Dentry cache hash table entries: 1048576 (order: 11, 8388608 bytes, linear)
[    0.000000] Inode-cache hash table entries: 524288 (order: 10, 4194304 bytes, linear)
[    0.000000] mem auto-init: stack:all(zero), heap alloc:off, heap free:off
[    0.000000] software IO TLB: mapped [mem 0x00000000fbfe0000-0x00000000fffe0000] (64MB)
[    0.000000] Memory: 7525864K/8133248K available (19328K kernel code, 4066K rwdata, 10040K rodata, 7616K init, 521K bss, 345240K reserved, 262144K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=6, Nodes=1
[    0.000000] trace event string verifier disabled
[    0.000000] rcu: Preemptible hierarchical RCU implementation.
[    0.000000] rcu:     RCU event tracing is enabled.
[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=6.
[    0.000000]  Trampoline variant of Tasks RCU enabled.
[    0.000000]  Rude variant of Tasks RCU enabled.
[    0.000000]  Tracing variant of Tasks RCU enabled.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=6
[    0.000000] NR_IRQS: 64, nr_irqs: 64, preallocated irqs: 0
[    0.000000] GICv3: GIC: Using split EOI/Deactivate mode
[    0.000000] GICv3: 960 SPIs implemented
[    0.000000] GICv3: 0 Extended SPIs implemented
[    0.000000] GICv3: Distributor has no Range Selector support
[    0.000000] Root IRQ handler: gic_handle_irq
[    0.000000] GICv3: 16 PPIs implemented
[    0.000000] GICv3: CPU0: found redistributor 0 region 0:0x000000000f440000
[    0.000000] arch_timer: cp15 timer(s) running at 31.25MHz (phys).
[    0.000000] clocksource: arch_sys_counter: mask: 0xffffffffffffff max_cycles: 0xe6a171046, max_idle_ns: 881590405314 ns
[    0.000001] sched_clock: 56 bits at 31MHz, resolution 32ns, wraps every 4398046511088ns
[    0.000379] Console: colour dummy device 80x25
[    0.000446] Calibrating delay loop (skipped), value calculated using timer frequency.. 62.50 BogoMIPS (lpj=125000)
[    0.000453] pid_max: default: 32768 minimum: 301
[    0.000490] LSM: Security Framework initializing
[    0.000515] Yama: becoming mindful.
[    0.000530] SELinux:  Initializing.
[    0.000612] Mount-cache hash table entries: 16384 (order: 5, 131072 bytes, linear)
[    0.000625] Mountpoint-cache hash table entries: 16384 (order: 5, 131072 bytes, linear)
[    0.001751] rcu: Hierarchical SRCU implementation.
[    0.004084] Tegra Revision: A01 SKU: 213 CPU Process: 0 SoC Process: 0
[    0.004352] Remapping and enabling EFI services.
[    0.005171] smp: Bringing up secondary CPUs ...
[    0.005671] Detected PIPT I-cache on CPU1
[    0.005715] GICv3: CPU1: found redistributor 100 region 0:0x000000000f460000
[    0.005751] CPU1: Booted secondary processor 0x0000000100 [0x410fd421]
[    0.006221] Detected PIPT I-cache on CPU2
[    0.006233] GICv3: CPU2: found redistributor 200 region 0:0x000000000f480000
[    0.006247] CPU2: Booted secondary processor 0x0000000200 [0x410fd421]
[    0.006660] Detected PIPT I-cache on CPU3
[    0.006669] GICv3: CPU3: found redistributor 300 region 0:0x000000000f4a0000
[    0.006683] CPU3: Booted secondary processor 0x0000000300 [0x410fd421]
[    0.009133] Detected PIPT I-cache on CPU4
[    0.009159] GICv3: CPU4: found redistributor 10200 region 0:0x000000000f500000
[    0.009187] CPU4: Booted secondary processor 0x0000010200 [0x410fd421]
[    0.009673] Detected PIPT I-cache on CPU5
[    0.009684] GICv3: CPU5: found redistributor 10300 region 0:0x000000000f520000
[    0.009700] CPU5: Booted secondary processor 0x0000010300 [0x410fd421]
[    0.009756] smp: Brought up 1 node, 6 CPUs
[    0.009760] SMP: Total of 6 processors activated.
[    0.009763] CPU features: detected: 32-bit EL0 Support
[    0.009765] CPU features: detected: Data cache clean to the PoU not required for I/D coherence
[    0.009767] CPU features: detected: Common not Private translations
[    0.009768] CPU features: detected: CRC32 instructions
[    0.009769] CPU features: detected: Data cache clean to Point of Persistence
[    0.009771] CPU features: detected: Generic authentication (architected algorithm)
[    0.009772] CPU features: detected: RCpc load-acquire (LDAPR)
[    0.009773] CPU features: detected: LSE atomic instructions
[    0.009774] CPU features: detected: Privileged Access Never
[    0.009775] CPU features: detected: RAS Extension Support
[    0.009778] CPU features: detected: Speculative Store Bypassing Safe (SSBS)
[    0.045727] CPU: All CPU(s) started at EL2
[    0.048930] devtmpfs: initialized
[    0.068184] KASLR enabled
[    0.068407] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    0.068441] futex hash table entries: 2048 (order: 5, 131072 bytes, linear)
[    0.073474] pinctrl core: initialized pinctrl subsystem
[    0.074521] SMBIOS 3.6.0 present.
[    0.074532] DMI: NVIDIA NVIDIA Jetson Orin Nano Engineering Reference Developer Kit Super/Jetson, BIOS v36.4.4 10/01/2024
[    0.075109] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    0.077072] DMA: preallocated 1024 KiB GFP_KERNEL pool for atomic allocations
[    0.077204] DMA: preallocated 1024 KiB GFP_KERNEL|GFP_DMA pool for atomic allocations
[    0.077291] DMA: preallocated 1024 KiB GFP_KERNEL|GFP_DMA32 pool for atomic allocations
[    0.077414] audit: initializing netlink subsys (disabled)
[    0.077606] audit: type=2000 audit(0.076:1): state=initialized audit_enabled=0 res=1
[    0.079554] thermal_sys: Registered thermal governor 'step_wise'
[    0.079556] thermal_sys: Registered thermal governor 'user_space'
[    0.079558] thermal_sys: Registered thermal governor 'power_allocator'
[    0.083581] cpuidle: using governor menu
[    0.083788] hw-breakpoint: found 6 breakpoint and 4 watchpoint registers.
[    0.083884] ASID allocator initialised with 32768 entries
[    0.085956] Serial: AMBA PL011 UART driver
[    0.098167] 31d0000.serial: ttyAMA0 at MMIO 0x31d0000 (irq = 117, base_baud = 0) is a SBSA
[    0.110095] platform bpmp: Fixing up cyclic dependency with 2c60000.external-memory-controller
[    0.119864] HugeTLB registered 1.00 GiB page size, pre-allocated 0 pages
[    0.119871] HugeTLB registered 32.0 MiB page size, pre-allocated 0 pages
[    0.119872] HugeTLB registered 2.00 MiB page size, pre-allocated 0 pages
[    0.119874] HugeTLB registered 64.0 KiB page size, pre-allocated 0 pages
[    0.120955] cryptd: max_cpu_qlen set to 1000
[    0.123117] ACPI: Interpreter disabled.
[    0.124400] VDD_1V8_AO: supplied by VDD_5V0_SYS
[    0.124564] VDD_3V3_AO: supplied by VDD_5V0_SYS
[    0.124785] VDD_AV10_HUB: supplied by VDD_5V0_SYS
[    0.125296] iommu: Default domain type: Translated 
[    0.125301] iommu: DMA domain TLB invalidation policy: strict mode 
[    0.125675] SCSI subsystem initialized
[    0.125952] vgaarb: loaded
[    0.126142] usbcore: registered new interface driver usbfs
[    0.126165] usbcore: registered new interface driver hub
[    0.126180] usbcore: registered new device driver usb
[    0.126589] pps_core: LinuxPPS API ver. 1 registered
[    0.126594] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.126607] PTP clock support registered
[    0.126694] EDAC MC: Ver: 3.0.0
[    0.127991] Registered efivars operations
[    0.128612] FPGA manager framework
[    0.128689] Advanced Linux Sound Architecture Driver Initialized.
[    0.129224] Bluetooth: Core ver 2.22
[    0.129258] NET: Registered PF_BLUETOOTH protocol family
[    0.129262] Bluetooth: HCI device and connection manager initialized
[    0.129270] Bluetooth: HCI socket layer initialized
[    0.129279] Bluetooth: L2CAP socket layer initialized
[    0.129293] Bluetooth: SCO socket layer initialized
[    0.129774] clocksource: Switched to clocksource arch_sys_counter
[    0.165094] VFS: Disk quotas dquot_6.6.0
[    0.165161] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)
[    0.165406] pnp: PnP ACPI: disabled
[    0.168346] NET: Registered PF_INET protocol family
[    0.168679] IP idents hash table entries: 131072 (order: 8, 1048576 bytes, linear)
[    0.170277] tcp_listen_portaddr_hash hash table entries: 4096 (order: 4, 65536 bytes, linear)
[    0.170374] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)
[    0.170406] TCP established hash table entries: 65536 (order: 7, 524288 bytes, linear)
[    0.170488] TCP bind hash table entries: 65536 (order: 8, 1048576 bytes, linear)
[    0.171828] TCP: Hash tables configured (established 65536 bind 65536)
[    0.172029] UDP hash table entries: 4096 (order: 5, 131072 bytes, linear)
[    0.172066] UDP-Lite hash table entries: 4096 (order: 5, 131072 bytes, linear)
[    0.172258] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    0.172707] RPC: Registered named UNIX socket transport module.
[    0.172712] RPC: Registered udp transport module.
[    0.172714] RPC: Registered tcp transport module.
[    0.172714] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.172733] PCI: CLS 0 bytes, default 64
[    0.173071] Unpacking initramfs...
[    0.178704] hw perfevents: enabled with armv8_cortex_a78 PMU driver, 7 counters available
[    0.179004] kvm [1]: IPA Size Limit: 48 bits
[    0.179044] kvm [1]: GICv3: no GICV resource entry
[    0.179052] kvm [1]: disabling GICv2 emulation
[    0.179081] kvm [1]: GIC system register CPU interface enabled
[    0.179154] kvm [1]: vgic interrupt IRQ9
[    0.179311] kvm [1]: VHE mode initialized successfully
[    0.182509] Initialise system trusted keyrings
[    0.182550] Key type blacklist registered
[    0.182671] workingset: timestamp_bits=42 max_order=21 bucket_order=0
[    0.185981] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    0.186428] NFS: Registering the id_resolver key type
[    0.186455] Key type id_resolver registered
[    0.186459] Key type id_legacy registered
[    0.186521] nfs4filelayout_init: NFSv4 File Layout Driver Registering...
[    0.186548] nfs4flexfilelayout_init: NFSv4 Flexfile Layout Driver Registering...
[    0.186578] ntfs: driver 2.1.32 [Flags: R/O].
[    0.186859] 9p: Installing v9fs 9p2000 file system support
[    0.187560] integrity: Platform Keyring initialized
[    0.200449] Key type asymmetric registered
[    0.200460] Asymmetric key parser 'x509' registered
[    0.200606] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 245)
[    0.200616] io scheduler mq-deadline registered
[    0.200624] io scheduler kyber registered
[    0.211656] EINJ: ACPI disabled.
[    0.225342] Serial: 8250/16550 driver, 4 ports, IRQ sharing enabled
[    0.227394] SuperH (H)SCI(F) driver initialized
[    0.227765] msm_serial: driver initialized
[    0.228622] printk: console [ttyTCU0] enabled
[    0.229739] arm-smmu 8000000.iommu: probing hardware configuration...
[    0.229748] arm-smmu 8000000.iommu: SMMUv2 with:
[    0.229756] arm-smmu 8000000.iommu:  stage 1 translation
[    0.229758] arm-smmu 8000000.iommu:  stage 2 translation
[    0.229771] arm-smmu 8000000.iommu:  nested translation
[    0.229775] arm-smmu 8000000.iommu:  stream matching with 128 register groups
[    0.229782] arm-smmu 8000000.iommu:  128 context banks (0 stage-2 only)
[    0.229798] arm-smmu 8000000.iommu:  Supported page sizes: 0x61311000
[    0.229801] arm-smmu 8000000.iommu:  Stage-1: 48-bit VA -> 48-bit IPA
[    0.229804] arm-smmu 8000000.iommu:  Stage-2: 48-bit IPA -> 48-bit PA
[    0.230904] arm-smmu 10000000.iommu: probing hardware configuration...
[    0.230909] arm-smmu 10000000.iommu: SMMUv2 with:
[    0.230913] arm-smmu 10000000.iommu:         stage 1 translation
[    0.230916] arm-smmu 10000000.iommu:         stage 2 translation
[    0.230918] arm-smmu 10000000.iommu:         nested translation
[    0.230925] arm-smmu 10000000.iommu:         stream matching with 128 register groups
[    0.230930] arm-smmu 10000000.iommu:         128 context banks (0 stage-2 only)
[    0.230941] arm-smmu 10000000.iommu:         Supported page sizes: 0x61311000
[    0.230944] arm-smmu 10000000.iommu:         Stage-1: 48-bit VA -> 48-bit IPA
[    0.230948] arm-smmu 10000000.iommu:         Stage-2: 48-bit IPA -> 48-bit PA
[    0.231354] arm-smmu 12000000.iommu: probing hardware configuration...
[    0.231358] arm-smmu 12000000.iommu: SMMUv2 with:
[    0.231359] arm-smmu 12000000.iommu:         stage 1 translation
[    0.231360] arm-smmu 12000000.iommu:         stage 2 translation
[    0.231361] arm-smmu 12000000.iommu:         nested translation
[    0.231364] arm-smmu 12000000.iommu:         stream matching with 128 register groups
[    0.231367] arm-smmu 12000000.iommu:         128 context banks (0 stage-2 only)
[    0.231372] arm-smmu 12000000.iommu:         Supported page sizes: 0x61311000
[    0.231373] arm-smmu 12000000.iommu:         Stage-1: 48-bit VA -> 48-bit IPA
[    0.231374] arm-smmu 12000000.iommu:         Stage-2: 48-bit IPA -> 48-bit PA
[    0.239437] loop: module loaded
[    0.240513] megasas: 07.717.02.00-rc1
[    0.244973] tun: Universal TUN/TAP device driver, 1.6
[    0.245625] thunder_xcv, ver 1.0
[    0.245652] thunder_bgx, ver 1.0
[    0.245679] nicpf, ver 1.0
[    0.246625] hclge is initializing
[    0.246658] hns3: Hisilicon Ethernet Network Driver for Hip08 Family - version
[    0.246666] hns3: Copyright (c) 2017 Huawei Corporation.
[    0.246713] e1000: Intel(R) PRO/1000 Network Driver
[    0.246719] e1000: Copyright (c) 1999-2006 Intel Corporation.
[    0.246752] e1000e: Intel(R) PRO/1000 Network Driver
[    0.246757] e1000e: Copyright(c) 1999 - 2015 Intel Corporation.
[    0.246785] igb: Intel(R) Gigabit Ethernet Network Driver
[    0.246792] igb: Copyright (c) 2007-2014 Intel Corporation.
[    0.246810] igbvf: Intel(R) Gigabit Virtual Function Network Driver
[    0.246816] igbvf: Copyright (c) 2009 - 2012 Intel Corporation.
[    0.247042] sky2: driver version 1.30
[    0.247774] VFIO - User Level meta-driver version: 0.3
[    0.249284] ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
[    0.249296] ehci-pci: EHCI PCI platform driver
[    0.249329] ehci-platform: EHCI generic platform driver
[    0.249413] ehci-orion: EHCI orion driver
[    0.249479] ehci-exynos: EHCI Exynos driver
[    0.249535] ohci_hcd: USB 1.1 'Open' Host Controller (OHCI) Driver
[    0.249564] ohci-pci: OHCI PCI platform driver
[    0.249585] ohci-platform: OHCI generic platform driver
[    0.249654] ohci-exynos: OHCI Exynos driver
[    0.250124] usbcore: registered new interface driver usb-storage
[    0.252181] i2c_dev: i2c /dev entries driver
[    0.253594] pps pps0: new PPS source ktimer
[    0.253602] pps pps0: ktimer PPS source registered
[    0.253609] pps_ldisc: PPS line discipline registered
[    0.255852] device-mapper: ioctl: 4.45.0-ioctl (2021-03-22) initialised: dm-devel@redhat.com
[    0.257995] sdhci: Secure Digital Host Controller Interface driver
[    0.257999] sdhci: Copyright(c) Pierre Ossman
[    0.258480] Synopsys Designware Multimedia Card Interface Driver
[    0.259125] sdhci-pltfm: SDHCI platform and OF driver helper
[    0.260318] ledtrig-cpu: registered to indicate activity on CPUs
[    0.261531] SMCCC: SOC_ID: ID = jep106:036b:0234 Revision = 0x00000401
[    0.262100] tegra-bpmp bpmp: Adding to iommu group 0
[    0.263449] tegra-bpmp bpmp: firmware: e941463f35523d12ee54-da583751bbf
[    0.332840] Freeing initrd memory: 8048K
[    2.307316] clocksource: tsc: mask: 0xffffffffffffff max_cycles: 0xe6a171046, max_idle_ns: 881590405314 ns
[    2.307340] clocksource: osc: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 49772407460 ns
[    2.307343] clocksource: usec: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 1911260446275 ns
[    2.307534] hid: raw HID events driver (C) Jiri Kosina
[    2.307865] usbcore: registered new interface driver usbhid
[    2.307871] usbhid: USB HID core driver
[    2.311379] optee: probing for conduit method.
[    2.311428] optee: revision 4.2
[    2.370044] optee: dynamic shared memory is enabled
[    2.370286] optee: initialized driver
[    2.372076] usbcore: registered new interface driver snd-usb-audio
[    2.373401] NET: Registered PF_PACKET protocol family
[    2.373900] Bluetooth: RFCOMM TTY layer initialized
[    2.373930] Bluetooth: RFCOMM socket layer initialized
[    2.373956] Bluetooth: RFCOMM ver 1.11
[    2.374248] 9pnet: Installing 9P2000 support
[    2.374349] Key type dns_resolver registered
[    2.375173] printk: console [ttyTCU0]: printing thread started
[    2.375328] Loading compiled-in X.509 certificates
[    2.378166] integrity: Loading X.509 certificate: UEFI:db
[    2.381231] integrity: Loaded X.509 cert 'QUALGO DB uefi1: e0eadae51fef964555638d631fa74092a49094ac'
[    2.381237] integrity: Loading X.509 certificate: UEFI:db
[    2.381813] integrity: Loaded X.509 cert 'QUALGO DB uefi2: a47adb9c31f1d2b2473fbf2d483b1445f0dbf846'
[    2.381815] integrity: Loading X.509 certificate: UEFI:db
[    2.382362] integrity: Loaded X.509 cert 'QUALGO DB kernel: d93f543ab1b34ad1e075270515149929ff915890'
[    2.411544] tegra-gpcdma 2600000.dma-controller: Adding to iommu group 1
[    2.412892] tegra-gpcdma 2600000.dma-controller: GPC DMA driver register 31 channels
[    2.414211] serial-tegra 3100000.serial: RX in PIO mode
[    2.414217] serial-tegra 3100000.serial: TX in PIO mode
[    2.414279] 3100000.serial: ttyTHS1 at MMIO 0x3100000 (irq = 112, base_baud = 0) is a TEGRA_UART
[    2.414818] 3140000.serial: ttyTHS2 at MMIO 0x3140000 (irq = 113, base_baud = 0) is a TEGRA_UART
[    2.416652] tegra_rtc c2a0000.rtc: registered as rtc1
[    2.416659] tegra_rtc c2a0000.rtc: Tegra internal Real Time Clock
[    2.417059] tegra-i2c 3160000.i2c: Adding to iommu group 1
[    2.420298] tegra-i2c 3180000.i2c: Adding to iommu group 1
[    2.422263] tegra-i2c 31b0000.i2c: Adding to iommu group 1
[    2.424019] tegra-i2c c240000.i2c: Adding to iommu group 1
[    2.425571] i2c 1-0025: Fixing up cyclic dependency with 3520000.padctl
[    2.426185] tegra-i2c c250000.i2c: Adding to iommu group 1
[    2.448893] cpufreq: cpufreq_online: CPU4: Running at unlisted initial frequency: 1772000 KHz, changing to: 1728000 KHz
[    2.452428] tegra-xusb 3610000.usb: Adding to iommu group 2
[    2.468228] tegra-xusb 3610000.usb: Firmware timestamp: 2023-02-10 03:48:10 UTC
[    2.468237] tegra-xusb 3610000.usb: xHCI Host Controller
[    2.468250] tegra-xusb 3610000.usb: new USB bus registered, assigned bus number 1
[    2.469001] tegra-xusb 3610000.usb: hcc params 0x0180ff05 hci version 0x120 quirks 0x0000000000010810
[    2.469022] tegra-xusb 3610000.usb: irq 124, io mem 0x03610000
[    2.469148] tegra-xusb 3610000.usb: xHCI Host Controller
[    2.469152] tegra-xusb 3610000.usb: new USB bus registered, assigned bus number 2
[    2.469155] tegra-xusb 3610000.usb: Host supports USB 3.1 Enhanced SuperSpeed
[    2.469430] hub 1-0:1.0: USB hub found
[    2.469448] hub 1-0:1.0: 4 ports detected
[    2.471096] hub 2-0:1.0: USB hub found
[    2.471113] hub 2-0:1.0: 4 ports detected
[    2.472677] sdhci-tegra 3400000.mmc: Adding to iommu group 3
[    2.473154] irq: IRQ228: trimming hierarchy from :bus@0:pmc@c360000
[    2.473211] irq: IRQ229: trimming hierarchy from :bus@0:interrupt-controller@f400000-1
[    2.473271] input: gpio-keys as /devices/platform/gpio-keys/input/input0
[    2.476922] sdhci-tegra 3400000.mmc: Got CD GPIO
[    2.521846] irq: IRQ230: trimming hierarchy from :bus@0:interrupt-controller@f400000-1
[    2.522093] mmc0: SDHCI controller on 3400000.mmc [3400000.mmc] using ADMA 64-bit
[    2.805769] usb 1-2: new high-speed USB device number 2 using tegra-xusb
[    2.976471] hub 1-2:1.0: USB hub found
[    2.977886] hub 1-2:1.0: 4 ports detected
[    3.090932] usb 2-1: new SuperSpeed Plus Gen 2x1 USB device number 2 using tegra-xusb
[    3.139539] hub 2-1:1.0: USB hub found
[    3.141992] hub 2-1:1.0: 4 ports detected
[    3.245770] usb 1-3: new full-speed USB device number 3 using tegra-xusb
[   14.944654] ALSA device list:
[   14.944659]   No soundcards found.
[   14.945669] Freeing unused kernel memory: 7616K
[   14.945732] Run /init as init process
Waiting for APP_b partition............[FAIL]
insmod /lib/modules/5.15.148-l4t-r36.4.4-1012.12+gc8a82765359e/kernel/drivers/nvme/host/nvme-core.ko 
insmod /lib/modules/5.15.148-l4t-r36.4.4-1012.12+gc8a82765359e/kernel/drivers/nvme/host/nvme.ko 
insmod /lib/modules/5.15.148-l4t-r36.4.4-1012.12+gc8a82765359e/kernel/drivers/phy/tegra/phy-tegra194-p2u.ko 
insmod /lib/modules/5.15.148-l4t-r36.4.4-1012.12+gc8a82765359e/kernel/drivers/pci/controller/dwc/pcie-tegra194.ko 
[   20.029509] tegra194-pcie 140a0000.pcie: Adding to iommu group 4
[   20.139510] tegra194-pcie 140a0000.pcie: host bridge /bus@0/pcie@140a0000 ranges:
[   20.139536] tegra194-pcie 140a0000.pcie:      MEM 0x3240000000..0x3527ffffff -> 0x3240000000
[   20.139543] tegra194-pcie 140a0000.pcie:      MEM 0x3528000000..0x352fffffff -> 0x0040000000
[   20.139546] tegra194-pcie 140a0000.pcie:       IO 0x002a100000..0x002a1fffff -> 0x002a100000
[   20.140032] tegra194-pcie 140a0000.pcie: iATU unroll: enabled
[   20.140034] tegra194-pcie 140a0000.pcie: Detected iATU regions: 8 outbound, 2 inbound
[   20.245943] tegra194-pcie 140a0000.pcie: Link up
[   20.248771] tegra194-pcie 140a0000.pcie: Link up
[   20.248837] tegra194-pcie 140a0000.pcie: PCI host bridge to bus 0008:00
[   20.248842] pci_bus 0008:00: root bus resource [io  0x0000-0xfffff] (bus address [0x2a100000-0x2a1fffff])
[   20.248846] pci_bus 0008:00: root bus resource [mem 0x3528000000-0x352fffffff] (bus address [0x40000000-0x47ffffff])
[   20.248850] pci_bus 0008:00: root bus resource [bus 00-ff]
[   20.248852] pci_bus 0008:00: root bus resource [mem 0x3240000000-0x3527ffffff pref]
[   20.248903] pci 0008:00:00.0: [10de:229c] type 01 class 0x060400
[   20.249058] pci 0008:00:00.0: PME# supported from D0 D3hot
[   20.252283] pci 0008:01:00.0: [10ec:8168] type 00 class 0x020000
[   20.252440] pci 0008:01:00.0: reg 0x10: initial BAR value 0x00000000 invalid
[   20.252442] pci 0008:01:00.0: reg 0x10: [io  size 0x0100]
[   20.252624] pci 0008:01:00.0: reg 0x18: [mem 0x00000000-0x00000fff 64bit]
[   20.252742] pci 0008:01:00.0: reg 0x20: [mem 0x00000000-0x00003fff 64bit]
[   20.253726] pci 0008:01:00.0: supports D1 D2
[   20.253727] pci 0008:01:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[   20.268513] pci 0008:00:00.0: BAR 14: assigned [mem 0x3528000000-0x35280fffff]
[   20.268518] pci 0008:00:00.0: BAR 13: assigned [io  0x1000-0x1fff]
[   20.268522] pci 0008:01:00.0: BAR 4: assigned [mem 0x3528000000-0x3528003fff 64bit]
[   20.268615] pci 0008:01:00.0: BAR 2: assigned [mem 0x3528004000-0x3528004fff 64bit]
[   20.268708] pci 0008:01:00.0: BAR 0: assigned [io  0x1000-0x10ff]
[   20.268737] pci 0008:00:00.0: PCI bridge to [bus 01-ff]
[   20.268740] pci 0008:00:00.0:   bridge window [io  0x1000-0x1fff]
[   20.268744] pci 0008:00:00.0:   bridge window [mem 0x3528000000-0x35280fffff]
[   20.268834] pcieport 0008:00:00.0: Adding to iommu group 4
[   20.268921] pcieport 0008:00:00.0: PME: Signaling with IRQ 189
[   20.269453] pcieport 0008:00:00.0: AER: enabled with IRQ 189
[   20.269738] tegra194-pcie 14100000.pcie: Adding to iommu group 5
[   20.270706] irq: IRQ231: trimming hierarchy from :bus@0:interrupt-controller@f400000-1
[   20.272831] tegra194-pcie 14100000.pcie: host bridge /bus@0/pcie@14100000 ranges:
[   20.272849] tegra194-pcie 14100000.pcie:      MEM 0x2080000000..0x20a7ffffff -> 0x2080000000
[   20.272855] tegra194-pcie 14100000.pcie:      MEM 0x20a8000000..0x20afffffff -> 0x0040000000
[   20.272859] tegra194-pcie 14100000.pcie:       IO 0x0030100000..0x00301fffff -> 0x0030100000
[   20.273330] tegra194-pcie 14100000.pcie: iATU unroll: enabled
[   20.273334] tegra194-pcie 14100000.pcie: Detected iATU regions: 8 outbound, 2 inbound
[   20.377941] tegra194-pcie 14100000.pcie: Link up
[   20.380421] tegra194-pcie 14100000.pcie: Link up
[   20.380476] tegra194-pcie 14100000.pcie: PCI host bridge to bus 0001:00
[   20.380481] pci_bus 0001:00: root bus resource [io  0x100000-0x1fffff] (bus address [0x30100000-0x301fffff])
[   20.380484] pci_bus 0001:00: root bus resource [mem 0x20a8000000-0x20afffffff] (bus address [0x40000000-0x47ffffff])
[   20.380488] pci_bus 0001:00: root bus resource [bus 00-ff]
[   20.380489] pci_bus 0001:00: root bus resource [mem 0x2080000000-0x20a7ffffff pref]
[   20.380536] pci 0001:00:00.0: [10de:229e] type 01 class 0x060400
[   20.380706] pci 0001:00:00.0: PME# supported from D0 D3hot
[   20.383797] pci 0001:01:00.0: [10ec:c822] type 00 class 0x028000
[   20.383969] pci 0001:01:00.0: reg 0x10: [io  0x100000-0x1000ff]
[   20.384171] pci 0001:01:00.0: reg 0x18: [mem 0x20a8000000-0x20a800ffff 64bit]
[   20.385196] pci 0001:01:00.0: supports D1 D2
[   20.385197] pci 0001:01:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[   20.400499] pci 0001:00:00.0: BAR 14: assigned [mem 0x20a8000000-0x20a80fffff]
[   20.400503] pci 0001:00:00.0: BAR 13: assigned [io  0x100000-0x100fff]
[   20.400506] pci 0001:01:00.0: BAR 2: assigned [mem 0x20a8000000-0x20a800ffff 64bit]
[   20.400609] pci 0001:01:00.0: BAR 0: assigned [io  0x100000-0x1000ff]
[   20.400639] pci 0001:00:00.0: PCI bridge to [bus 01-ff]
[   20.400643] pci 0001:00:00.0:   bridge window [io  0x100000-0x100fff]
[   20.400647] pci 0001:00:00.0:   bridge window [mem 0x20a8000000-0x20a80fffff]
[   20.400738] pcieport 0001:00:00.0: Adding to iommu group 5
[   20.400825] pcieport 0001:00:00.0: PME: Signaling with IRQ 191
[   20.401364] pcieport 0001:00:00.0: AER: enabled with IRQ 191
[   20.401685] tegra194-pcie 14160000.pcie: Adding to iommu group 6
[   20.403247] tegra194-pcie 14160000.pcie: host bridge /bus@0/pcie@14160000 ranges:
[   20.403263] tegra194-pcie 14160000.pcie:      MEM 0x2140000000..0x2427ffffff -> 0x2140000000
[   20.403270] tegra194-pcie 14160000.pcie:      MEM 0x2428000000..0x242fffffff -> 0x0040000000
[   20.403274] tegra194-pcie 14160000.pcie:       IO 0x0036100000..0x00361fffff -> 0x0036100000
[   20.403578] tegra194-pcie 14160000.pcie: iATU unroll: enabled
[   20.403580] tegra194-pcie 14160000.pcie: Detected iATU regions: 8 outbound, 2 inbound
[   20.509942] tegra194-pcie 14160000.pcie: Link up
[   20.510914] tegra194-pcie 14160000.pcie: Link up
[   20.510964] tegra194-pcie 14160000.pcie: PCI host bridge to bus 0004:00
[   20.510969] pci_bus 0004:00: root bus resource [io  0x200000-0x2fffff] (bus address [0x36100000-0x361fffff])
[   20.510972] pci_bus 0004:00: root bus resource [mem 0x2428000000-0x242fffffff] (bus address [0x40000000-0x47ffffff])
[   20.510976] pci_bus 0004:00: root bus resource [bus 00-ff]
[   20.510978] pci_bus 0004:00: root bus resource [mem 0x2140000000-0x2427ffffff pref]
[   20.511020] pci 0004:00:00.0: [10de:229c] type 01 class 0x060400
[   20.511169] pci 0004:00:00.0: PME# supported from D0 D3hot
[   20.514302] pci 0004:01:00.0: [1d97:1202] type 00 class 0x010802
[   20.514493] pci 0004:01:00.0: reg 0x10: [mem 0x00000000-0x00003fff 64bit]
[   20.515719] pci 0004:01:00.0: PME# supported from D0 D3hot D3cold
[   20.519097] pci 0004:00:00.0: BAR 14: assigned [mem 0x2428000000-0x24280fffff]
[   20.519102] pci 0004:01:00.0: BAR 0: assigned [mem 0x2428000000-0x2428003fff 64bit]
[   20.519186] pci 0004:00:00.0: PCI bridge to [bus 01-ff]
[   20.519190] pci 0004:00:00.0:   bridge window [mem 0x2428000000-0x24280fffff]
[   20.519274] pcieport 0004:00:00.0: Adding to iommu group 6
[   20.519361] pcieport 0004:00:00.0: PME: Signaling with IRQ 193
[   20.519964] pcieport 0004:00:00.0: AER: enabled with IRQ 193
[   20.520208] nvme 0004:01:00.0: Adding to iommu group 6
[   20.520670] nvme nvme0: pci function 0004:01:00.0
[   20.520726] nvme 0004:01:00.0: enabling device (0000 -> 0002)
[   20.520811] tegra194-pcie 141e0000.pcie: Adding to iommu group 7
[   20.523331] tegra194-pcie 141e0000.pcie: host bridge /bus@0/pcie@141e0000 ranges:
[   20.523353] tegra194-pcie 141e0000.pcie:      MEM 0x3000000000..0x3227ffffff -> 0x3000000000
[   20.523359] tegra194-pcie 141e0000.pcie:      MEM 0x3228000000..0x322fffffff -> 0x0040000000
[   20.523362] tegra194-pcie 141e0000.pcie:       IO 0x003e100000..0x003e1fffff -> 0x003e100000
[   20.523868] tegra194-pcie 141e0000.pcie: iATU unroll: enabled
[   20.523872] tegra194-pcie 141e0000.pcie: Detected iATU regions: 8 outbound, 2 inbound
[   20.528827] nvme nvme0: allocated 16 MiB host memory buffer.
[   20.536230] nvme nvme0: 6/0/0 default/read/poll queues
[   20.540557]  nvme0n1: p1 p2 p3 p4 p5 p6 p7 p8 p9 p10 p11 p12 p13 p14 p15 p16
[   21.631858] tegra194-pcie 141e0000.pcie: Phy link never came up
[   22.633714] tegra194-pcie 141e0000.pcie: Phy link never came up
[   22.633808] tegra194-pcie 141e0000.pcie: PCI host bridge to bus 0007:00
[   22.633813] pci_bus 0007:00: root bus resource [io  0x300000-0x3fffff] (bus address [0x3e100000-0x3e1fffff])
[   22.633817] pci_bus 0007:00: root bus resource [mem 0x3228000000-0x322fffffff] (bus address [0x40000000-0x47ffffff])
[   22.633821] pci_bus 0007:00: root bus resource [bus 00-ff]
[   22.633822] pci_bus 0007:00: root bus resource [mem 0x3000000000-0x3227ffffff pref]
[   22.633872] pci 0007:00:00.0: [10de:229a] type 01 class 0x060400
[   22.634030] pci 0007:00:00.0: PME# supported from D0 D3hot
[   22.639848] pci 0007:00:00.0: PCI bridge to [bus 01-ff]
[   22.639973] pcieport 0007:00:00.0: Adding to iommu group 7
[   22.640072] pcieport 0007:00:00.0: PME: Signaling with IRQ 195
[   22.640610] pcieport 0007:00:00.0: AER: enabled with IRQ 195
[   22.640871] pci_bus 0007:01: busn_res: [bus 01-ff] is released
[   22.640966] pci 0007:00:00.0: Removing from iommu group 7
[   22.640978] pci_bus 0007:00: busn_res: [bus 00-ff] is released
insmod /lib/modules/5.15.148-l4t-r36.4.4-1012.12+gc8a82765359e/updates/drivers/net/ethernet/realtek/r8168/r8168.ko 
[   23.146790] r8168: loading out-of-tree module taints kernel.
[   23.148565] r8168 0008:01:00.0: Adding to iommu group 4
[   23.148649] r8168 Gigabit Ethernet driver 8.053.00-NAPI loaded
[   23.148717] r8168 0008:01:00.0: enabling device (0000 -> 0003)
[   23.164997] r8168: This product is covered by one or more of the following patents: US6,570,884, US6,115,776, and US6,327,625.
[   23.167057] r8168  Copyright (C) 2024 Realtek NIC software team <nicfae@realtek.com> 
[   23.167057]  This program comes with ABSOLUTELY NO WARRANTY; for details, please see <http://www.gnu.org/licenses/>. 
[   23.167057]  This is free software, and you are welcome to redistribute it undeitrerts] ain cong IFAnditioCE=ns;0 sehttp://www.gnu.org/licenses/>. 
[   23.172643] eth0: 0xffff800008055000, 3c:6d:66:76:71:f1, IRQ 239
[   26.291217] r8168: eth0: link up
[initramfs] eth0 carrier=1
[initramfs] DHCP: udhcpc on eth0
udhcpc: started, v1.36.1
udhcpc: broadcasting discover
udhcpc: broadcasting select for 192.168.42.101, server 192.168.42.1
udhcpc: lease of 192.168.42.101 obtained from 192.168.42.1, lease time 600
/etc/udhcpc.d/50default: Adding DNS 8.8.8.8
[initramfs] DHCP: IPv4 configured
[initramfs] Mounting NFS root...
[initramfs] Switching to rootfs...
[   27.926566] systemd[1]: System time before build time, advancing clock.
[   27.965975] NET: Registered PF_INET6 protocol family
[   27.966652] Segment Routing with IPv6
[   27.966659] In-situ OAM (IOAM) with IPv6

Welcome to OE4Tegra Demonstration Distro 5.0.15+snapshot-6988157ad983978ffd6b12bcefedd4deaffdbbd1 (scarthgap)!
```