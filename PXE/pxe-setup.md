[Host]

1. DHCP server 
+ Install
```
$ sudo apt install isc-dhcp-server
```

+  Configuration modify /etc/default/isc-dhcp-server. And connect ethernet from host to device to get ethenet interface name (e.g: enp0s31f6)
```
hao-nna@QGU0011:~/uav-yocto-build$ cat  /etc/default/isc-dhcp-server
INTERFACESv4="enp0s31f6"
```

+ Add pxe details in dhcp conf file (/etc/dhcp/dhcpd.conf)
```
# /etc/dhcp/dhcpd.conf

# Global Settings
authoritative-name "example.com";
option domain;
option domain-name-servers 8.8.8.8, 8.8.4.4;
default-lease-time 600;
max-lease-time 7200;


subnet 192.168.42.0 netmask 255.255.255.0 {
    range 192.168.42.100 192.168.42.200;          # IP range for clients
    option routers 192.168.42.1;                   # Default gateway
    option broadcast-address 192.168.42.255;       # Broadcast address
    option domain-name-servers 8.8.8.8;            # DNS
    next-server 192.168.42.1;                      # IP of the PXE server (TFTP)
    filename "bootaa64.efi";                       # UEFI bootloader
}

```

+ sudo systemctl restart isc-dhcp-server

2. Setup TFTP Server
+ Install
```
$ sudo apt install -y tftpd-hpa
```
+ Configuration modify /etc/default/tftpd-hpa
```
# /etc/default/tftpd-hpa

TFTP_USERNAME="tftp"
TFTP_DIRECTORY="/tftp"
TFTP_ADDRESS=":69"
TFTP_OPTIONS="--secure --verbose --verbosity 5"
```

+ sudo systemctl restart tftpd-hpa

3. Setup NFS
```
$ cat /etc/exports 
/volume1/nfs_root 192.168.42.0/24(rw,sync,no_subtree_check,no_root_squash,insecure)

$ sudo exportfs -ra
$ sudo systemctl restart nfs-kernel-server
```

4. OS setup

+ RootFS
```
mkdir -p /volume1/nfs_root
tar xf tar xf build/tmp/deploy/images/jetson-orin-nano-devkit-nvme/demo-image-base-jetson-orin-nano-devkit-nvme.rootfs.tar.gz -C /volume1/nfs_root
```

+ copy Image, Initrd from rootfs and our EFI applications to /tftp folder. We can use /volume1/nfs_root/boot/{Image,intrd} and /volume1/nfs_root/EFI/BOOT/firstLoader.efi -> bootaa64.efi
```
/tftp/
├── bootaa64.efi
├── cmdline.txt
├── Image
├── initrd
└── secondLoader.enc
```

+ Add cmdline.txt file to describe bootargs, e.g:
```
root=/dev/nfs nfsroot=192.168.42.1:/volume1/nfs_root/ nfsopts=vers=3,tcp,nolock ip=dhcp net.ifnames=0
console=ttyTCU0,115200 firmware_class.path=/etc/firmware
```

[Target]

1. Reboot

2. Press ESC to enter UEFI menu

3. Select PXEv4

TODO: Set UEFI PXEv4 (MAC:3C6D667671F1) as primary boot