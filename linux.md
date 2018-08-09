# linux 

## mem_size的含义

## 内核启动信息

```
SF: Detected S25FL256L_64K with page size 256 Bytes, erase size 32 KiB, total 16 MiB
Disabling outer cache
Booting Linux on physical CPU 0x0
Linux version 4.4.39 (fhos@fh-linux) (gcc version 4.9.3 (fhos 2018.04.24) ) #1 SMP PREEMPT Tue Apr 24 11:22:50 CST 2018
CPU: ARMv7 Processor [414fc091] revision 1 (ARMv7), cr=10c5387d
CPU: PIPT / VIPT nonaliasing data cache, VIPT aliasing instruction cache
Machine model: Broadcom HR2 SVK (BCM956150K)
Ignoring memory range 0x60000000 - 0x80000000
cma: Reserved 32 MiB at 0x9d000000
Memory policy: Data cache writeback
CPU: All CPU(s) started in SVC mode.
PERCPU: Embedded 11 pages/cpu @dcbf6000 s15744 r8192 d21120 u45056
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 125984
Kernel command line: root=/dev/ram0 rw ramdisk_size=0x1c000000 rootdelay=3 maxcpus=1 mem=496M console=ttyS0,115200 rootfstype=ext4
PID hash table entries: 2048 (order: 1, 8192 bytes)
Dentry cache hash table entries: 65536 (order: 6, 262144 bytes)
Inode-cache hash table entries: 32768 (order: 5, 131072 bytes)
Memory: 414760K/507904K available (5018K kernel code, 174K rwdata, 1432K rodata, 228K init, 169K bss, 60376K reserved, 32768K cma-reserved)
Virtual kernel memory layout:
    vector  : 0xffff0000 - 0xffff1000   (   4 kB)
    fixmap  : 0xffc00000 - 0xfff00000   (3072 kB)
    vmalloc : 0xdf800000 - 0xff800000   ( 512 MB)
    lowmem  : 0xc0000000 - 0xdf000000   ( 496 MB)
    modules : 0xbf000000 - 0xc0000000   (  16 MB)
      .text : 0xc0008000 - 0xc0654ddc   (6452 kB)
      .init : 0xc0655000 - 0xc068e000   ( 228 kB)
      .data : 0xc068e000 - 0xc06b9a20   ( 175 kB)
       .bss : 0xc06b9a20 - 0xc06e3e24   ( 170 kB)
SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
Preemptible hierarchical RCU implementation.
	Build-time adjustment of leaf fanout to 32.
	RCU restricting CPUs from NR_CPUS=4 to nr_cpu_ids=1.
RCU: Adjusting geometry for rcu_fanout_leaf=32, nr_cpu_ids=1
NR_IRQS:16 nr_irqs:16 16
L2C-310 enabling early BRESP for Cortex-A9
L2C-310 full line of zeros enabled for Cortex-A9
L2C-310 dynamic clock gating enabled, standby mode enabled
L2C-310 cache controller enabled, 8 ways, 128 kB
L2C-310: CACHE_ID 0x410000c9, AUX_CTRL 0x4e120001
sched_clock: 64 bits at 200MHz, resolution 5ns, wraps every 4398046511102ns
clocksource: arm_global_timer: mask: 0xffffffffffffffff max_cycles: 0x2e2049dc38, max_idle_ns: 440795209465 ns
Calibrating delay loop... 795.44 BogoMIPS (lpj=3977216)
pid_max: default: 4096 minimum: 301
Mount-cache hash table entries: 1024 (order: 0, 4096 bytes)
Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes)
CPU: Testing write buffer coherency: ok
CPU0: thread -1, cpu 0, socket 0, mpidr 80000000
Setting up static identity map for 0x80008280 - 0x800082d8
Brought up 1 CPUs
SMP: Total of 1 processors activated (795.44 BogoMIPS).
CPU: All CPU(s) started in SVC mode.
devtmpfs: initialized
clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns
NET: Registered protocol family 16
DMA: preallocated 16384 KiB pool for atomic coherent allocations
SCSI subsystem initialized
libphy: iproc_ccb_mdiobus: probed
libphy: iproc_ccb_mdiobus: probed
NVRAM: map 0x1e0c0000
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
pps_core: LinuxPPS API ver. 1 registered
pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
PTP clock support registered
clocksource: Switched to clocksource arm_global_timer
NET: Registered protocol family 2
TCP established hash table entries: 4096 (order: 2, 16384 bytes)
TCP bind hash table entries: 4096 (order: 3, 32768 bytes)
TCP: Hash tables configured (established 4096 bind 4096)
UDP hash table entries: 256 (order: 1, 8192 bytes)
UDP-Lite hash table entries: 256 (order: 1, 8192 bytes)
NET: Registered protocol family 1
RPC: Registered named UNIX socket transport module.
RPC: Registered udp transport module.
RPC: Registered tcp transport module.
RPC: Registered tcp NFSv4.1 backchannel transport module.
Trying to unpack rootfs image as initramfs...
rootfs image is not initramfs (no cpio magic); looks like an initrd
Freeing initrd memory: 48800K (c8000000 - cafa8000)
futex hash table entries: 16 (order: -2, 1024 bytes)
NFS: Registering the id_resolver key type
Key type id_resolver registered
Key type id_legacy registered
Installing knfsd (copyright (C) 1996 okir@monad.swb.de).
ntfs: driver 2.1.32 [Flags: R/O].
jffs2: version 2.2. (NAND) © 2001-2006 Red Hat, Inc.
Block layer SCSI generic (bsg) driver version 0.4 loaded (major 250)
io scheduler noop registered
io scheduler deadline registered
io scheduler cfq registered (default)
iproc-gpio 18000060.gpio: gpio_cca intr_ioaddr: df982000
iproc-gpio 18000060.gpio: gpio_cca iaddr: df984060
iproc gpiochip add gpio_cca
iproc-gpio 48002000.gpio: gpio_ccb iaddr: df986000
iproc gpiochip add gpio_ccb
PCI host bridge /pcie@18012000 ranges:
  No bus range found for /pcie@18012000, using [bus 00-ff]
  MEM 0x08000000..0x0fffffff -> 0x08000000
iproc-pcie 18012000.pcie: PCI host bridge to bus 0000:00
pci_bus 0000:00: root bus resource [bus 00-ff]
pci_bus 0000:00: root bus resource [mem 0x08000000-0x0fffffff]
iproc-pcie 18012000.pcie: in EP mode, hdr=0x80
iproc-pcie 18012000.pcie: no PCIe EP device detected
iproc-pcie 18012000.pcie: PCIe controller setup failed
iproc-pcie: probe of 18012000.pcie failed with error -14
Serial: 8250/16550 driver, 2 ports, IRQ sharing enabled
18000300.serial: ttyS1 at MMIO 0x18000300 (irq = 18, base_baud = 3125000) is a 16550A
console [ttyS0] disabled
18000400.serial: ttyS0 at MMIO 0x18000400 (irq = 18, base_baud = 3125000) is a 16550A
console [ttyS0] enabled
brd: module loaded
st: Version 20101219, fixed bufsize 32768, s/g segs 256
S29GL-MTD: NOR_INTERFACE Enabled
S29GL-MTD probing 32bit FLASH
S29GL-MTD probing 16bit FLASH
S29GL-MTD NO FLASH found!
nand: device found, Manufacturer ID: 0x2c, Chip ID: 0xd3
nand: Micron MT29F8G08ADADAH4
nand: 1024 MiB, SLC, erase size: 128 KiB, page size: 2048, OOB size: 64
iproc_nand 18026000.nand: detected 1024MiB total, 128KiB blocks, 2KiB pages, 16B OOB, 8-bit, BCH-4
Bad block table found at page 524224, version 0x01
Bad block table found at page 524160, version 0x01
10 ofpart partitions found on MTD device brcmnand.0
Creating 10 MTD partitions on "brcmnand.0":
0x000000000000-0x000000200000 : "uboot image"
0x000000200000-0x000000600000 : "uboot env"
0x000000600000-0x000001000000 : "kern image"
0x000001000000-0x000001100000 : "device tree"
0x000001100000-0x000001200000 : "hardware information"
0x000001200000-0x000006200000 : "rootfs"
0x000006200000-0x000016200000 : "applications"
0x000016200000-0x000018200000 : "configs"
0x000018200000-0x00002c200000 : "user"
0x00002c200000-0x00003ff00000 : "logs"
iproc-qspi 18027200.spi: missing #bus-id property (default to 1)
iproc-qspi 18027200.spi: 1-lane output, 3-byte address
m25p80 spi1.0: unrecognized JEDEC id bytes: 01, 60, 19
Ethernet Channel Bonding Driver: v3.7.1 (April 27, 2011)
iproc_gmac_drv_probe enter :18022000.ethernet; id:0xffffffff; unit:0
et0: base_addr (0xdf82a000) irq (19)
etc_gmac_speed default GMAC0 speed: auto
etc_attach() mdio_init_time = 5
si_doattach chipid: 0x3f00db56
si_attach socitype(0x3) chip(0xdb56) chiprev(0x0) chippkg(0x0)
et0: chipattach: phyaddr(0x1)
et0: phy5221_fe_reset reset complete
eth0: Broadcom BCM5615x 10/100 Mbps Ethernet Controller 6.30.40 (TOB) (r)
iproc_gmac_init_module: et_rx_rate_limit set to 0x1
ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
ehci-pci: EHCI PCI platform driver
ehci-platform: EHCI generic platform driver
ohci_hcd: USB 1.1 'Open' Host Controller (OHCI) Driver
ohci-pci: OHCI PCI platform driver
ohci-platform: OHCI generic platform driver
usbcore: registered new interface driver usb-storage
i2c /dev entries driver
bcm-iproc-i2c 48000000.i2c: bus set to 100000 Hz
iproc-sp805-wdt 18039000.iproc_wdt: registration successful
iproc-sp805-wdt 18039000.iproc_wdt: timeout=60 sec, nowayout=0
sdhci: Secure Digital Host Controller Interface driver
sdhci: Copyright(c) Pierre Ossman
Netfilter messages via NETLINK v0.30.
nf_conntrack version 0.5.0 (7755 buckets, 31020 max)
ip_tables: (C) 2000-2006 Netfilter Core Team
arp_tables: (C) 2002 David S. Miller
NET: Registered protocol family 17
bridge: automatic filtering via arp/ip/ip6tables has been deprecated. Update your scripts to load br_netfilter if you need this.
Bridge firewalling registered
8021q: 802.1Q VLAN Support v1.8
Key type dns_resolver registered
Registering SWP/SWPB emulation handler
Waiting 3 sec before mounting root device...
RAMDISK: gzip image found at block 0
EXT4-fs (ram0): mounted filesystem with ordered data mode. Opts: (null)
VFS: Mounted root (ext4 filesystem) on device 1:0.
devtmpfs: mounted
Freeing unused kernel memory: 228K (c0655000 - c068e000)
EXT4-fs (ram0): re-mounted. Opts: errors=remount-ro,data=ordered
EXT4-fs (mtdblock6): mounted filesystem with ordered data mode. Opts: (null)
EXT4-fs (mtdblock7): mounted filesystem with ordered data mode. Opts: (null)
EXT4-fs (mtdblock8): mounted filesystem with ordered data mode. Opts: (null)
EXT4-fs (mtdblock9): mounted filesystem with ordered data mode. Opts: (null)
Initializing random number generator... random: dd: uninitialized urandom read (512 bytes read, 25 bits of entropy available)
done.
Starting network...
Starting OpenBSD Secure Shell server: sshd
  generating ssh RSA key...
random: ssh-keygen: uninitialized urandom read (32 bytes read, 25 bits of entropy available)
  generating ssh ECDSA key...
random: ssh-keygen: uninitialized urandom read (32 bytes read, 32 bits of entropy available)
  generating ssh DSA key...
random: ssh-keygen: uninitialized urandom read (32 bytes read, 32 bits of entropy available)
  generating ssh ED25519 key...
random: ssh-keygen: uninitialized urandom read (32 bytes read, 35 bits of entropy available)
random: sshd: uninitialized urandom read (32 bytes read, 35 bits of entropy available)
done.
Starting internet superserver: xinetd.
init board system
Fri Aug 25 00:00:00 UTC 2017
insmod /fhos/mods/linux-kernel-bde.ko
linux_kernel_bde: module license 'Proprietary' taints kernel.
Disabling lock debugging due to kernel taint
insmod /fhos/mods/linux-bcm-knet.ko
insmod /fhos/mods/linux-user-bde.ko
linux-kernel-bde (681): _get_cmic_ver: Not PCI device 0, type 20000180
random: snmpd: uninitialized urandom read (32 bytes read, 35 bits of entropy available)
loading /fhos/apps/snmpd -Lf /var/log/snmpd.log -p /run/snmpd.pid -c /etc/fhos/snmpd.conf, return 0
random: nonblocking pool is initialized
RTNETLINK answers: No such device
compiling time: Apr 28 2018 09:32:24
loading /fhos/apps/l2d -d -f /etc/fhos/l2d.conf, return 0
compiling time: Apr 28 2018 09:32:29
loading /fhos/apps/igmpd -d -f /etc/fhos/igmpd.conf, return 0
compiling time: Apr 28 2018 09:32:40
loading /fhos/apps/dhcpd -d -f /etc/fhos/dhcpd.conf, return 0
loading /fhos/apps/mstp -d -f /etc/fhos/mstpd.conf, return 0
creating new /var/db/ntpd.drift
loading /fhos/apps/ntpd -s -f /etc/fhos/ntpd.conf, return 0
2017/08/25 00:00:27 errors: UPGRADE: vty_read_config: failed to open configuration file /run/media/mtdblock7/upgrade.conf: No such file or directory
2017/08/25 00:00:27 errors: UPGRADE: can't open configuration file [/run/media/mtdblock7/upgrade.conf]
loading /fhos/apps/upgrade -d, return 0

Welcome to fhos 
fhos login: 
Welcome to fhos 
fhos login: root
Password: 
login[791]: root login on 'ttyS0'
```

## random: nonblocking pool is initialized

