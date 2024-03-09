## TP-Link TD-W9970v3(Turk Telekom)

![Untitled](https://github.com/onerc/reverse-engineering/assets/94126150/ca60d1ff-e409-41d1-b959-96d281586d6d)

A modem of many faces

## One model name, two products

According to Turk Telekom, this modem has model number W9970v3 (can still be seen in the [manual](https://www.turktelekom.com.tr/Documents/TP-Link-TD-W9970_kullanim_kilavuzu.pdf)), but in reality that model number belongs to [another modem](https://www.tp-link.com/en/home-networking/dsl-modem-router/td-w9970/v3/
).

Even the internals look different. Not sure why they chose the name of an existing model.

I guess TP-Link received so many questions/complaints about the _fake_ W9970v3 that they added additional information to the [Turkish page](https://www.tp-link.com/tr/home-networking/dsl-modem-router/td-w9970/v3/) regarding the situation.

>Önemli Bilgi ; Türk Telekom tarafından internet başvurusu dahilinde verilen TD-W9970V3 model ürün ile Web sitemizde yer alan TD-W9970 V3 modelleri birbirlerinden farklıdır. Türk Telekom tarafından verilen TD-W9970V3 modelin yazılım ve servis hizmetleri Sentim Bilişim firması tarafından sağlanmaktadır. İlgili firmaya http://www.sentim.com.tr/iletisim-destek/modem-destek/ iletişim bilgilerinden ulaşabilirsiniz..

In English:
>Important information ; The TD-W9970V3 model product provided by Türk Telekom within the internet application and the TD-W9970 V3 models on our website are different from each other. The software and services of the TD-W9970V3 model supplied by Türk Telekom are provided by Sentim Bilişim. You can reach the relevant company from the contact information http://www.sentim.com.tr/iletisim-destek/modem-destek/.

## Internals
![20201005_171827](https://github.com/onerc/reverse-engineering/assets/94126150/595b7814-f728-472a-b694-fc5c8778d548)

## Pinout
![UART](https://github.com/onerc/reverse-engineering/assets/94126150/b72547cf-0acd-4b82-9bc5-c84babe3b4fc)

## Dump
I had two subjects, one was running firmware version ```17.12.27.01005```, the other one was running version ```20.05.16.01006```. Curiosity killed the old one.

Dumping via CFE bootloader took ~7 hours. Folks at [@exploiteers](https://github.com/exploiteers)(big thanks!) trimmed/rebuilt the dump.


```
↪ binwalk TD-W9970.bin

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
131072        0x20000         JFFS2 filesystem, big endian
61866000      0x3B00010       XML document, version: "1.0"
62914576      0x3C00010       XML document, version: "1.0"
```


## Boot log
<details>

```
HELO
CPUI
L1CI
HELO
CPUI
L1CI
4.1601-1.0.38-116.15
DRAM
----
PHYS
STRF
400H
PHYE
DDR2
SIZ4
SIZ3
SIZ2
SIZ1
DINT
USYN
LSYN
MFAS
LMBE
RACE
PASS
----
ZBSS
CODE
DATA
L12F
MAIN
FPS0
B002
0001
B003
0236
NAN3
RFS2
NAN5


Base: 4.16_01
CFE version 1.0.38-116.15 for BCM963268 (32bit,SP,BE)
Build Date: 2020年 05月 16日 星期六 17:15:05 CST (root@tplink)
Copyright (C) 2000-2013 Broadcom Corporation.

Chip ID: BCM63168D0, MIPS: 400MHz, DDR: 400MHz, Bus: 200MHz
Main Thread: TP0
Memory Test Passed
Total Memory: 67108864 bytes (64MB)
Boot Address: 0xb8000000

NAND ECC Hamming, page size 0x800 bytes, spare size used 64 bytes
NAND flash device: ESMT, id 0xc8d1 block 128KB size 131072KB
Board IP address                  : 192.168.1.1:ffffff00
Host IP address                   : 192.168.1.100
Gateway IP address                :
Run from flash/host/tftp (f/h/c)  : f
Default host run file name        : vmlinux
Default host flash file name      : bcm963xx_fs_kernel
Boot delay (0-9 seconds)          : 3
Boot image (0=latest, 1=previous) : 0
Default host ramdisk file name    :
Default ramdisk store address     :
Board Id (0-29)                   : 963168XF
Number of MAC Addresses (1-32)    : 11
Base MAC Address                  : c5:05:c0:99:70:01
PSI Size (1-64) KBytes            : 24
Enable Backup PSI [0|1]           : 0
System Log Size (0-256) KBytes    : 0
Auxillary File System Size Percent: 0
Main Thread Number [0|1]          : 0

*** Press 't' to stop auto run (0.3 seconds) ***
CFE>
web info: Waiting for connection on socket 0.[J

CFE> help
Available commands:

dn                  Dump NAND contents along with spare area
phy                 Set memory or registers.
sm                  Set memory or registers.
dm                  Dump memory or registers.
db                  Dump bytes.
dh                  Dump half-words.
dw                  Dump words.
e                   Erase NAND flash
r                   Run program from flash image or from host depend on [f/h] flag
p                   Print boot line and board parameter info
c                   Change booline parameters
f                   Write image to the flash
i                   Erase persistent storage data
a                   Change board AFE ID
b                   Change board parameters
reset               Reset the board
pmdio               Pseudo MDIO access for external switches.
spi                 Legacy SPI access of external switch.
force               override chipid check for images.
help                Obtain help for CFE commands

For more information about a command, enter 'help command-name'
*** command status = 0
CFE> p
Board IP address                  : 192.168.1.1:ffffff00
Host IP address                   : 192.168.1.100
Gateway IP address                :
Run from flash/host/tftp (f/h/c)  : f
Default host run file name        : vmlinux
Default host flash file name      : bcm963xx_fs_kernel
Boot delay (0-9 seconds)          : 3
Boot image (0=latest, 1=previous) : 0
Default host ramdisk file name    :
Default ramdisk store address     :
Board Id (0-29)                   : 963168XF
Number of MAC Addresses (1-32)    : 11
Base MAC Address                  : c5:05:c0:99:70:01
PSI Size (1-64) KBytes            : 24
Enable Backup PSI [0|1]           : 0
System Log Size (0-256) KBytes    : 0
Auxillary File System Size Percent: 0
Main Thread Number [0|1]          : 0

*** command status = 0
CFE> reset

Resetting board in 0 seconds...
HELO
CPUI
L1CI
HELO
CPUI
L1CI
4.1601-1.0.38-116.15
DRAM
----
PHYS
STRF
400H
PHYE
DDR2
SIZ4
SIZ3
SIZ2
SIZ1
DINT
USYN
LSYN
MFAS
LMBE
RACE
PASS
----
ZBSS
CODE
DATA
L12F
MAIN
FPS0
B002
0001
B003
0236
NAN3
RFS2
NAN5


Base: 4.16_01
CFE version 1.0.38-116.15 for BCM963268 (32bit,SP,BE)
Build Date: 2020年 05月 16日 星期六 17:15:05 CST (root@tplink)
Copyright (C) 2000-2013 Broadcom Corporation.

Chip ID: BCM63168D0, MIPS: 400MHz, DDR: 400MHz, Bus: 200MHz
Main Thread: TP0
Memory Test Passed
Total Memory: 67108864 bytes (64MB)
Boot Address: 0xb8000000

NAND ECC Hamming, page size 0x800 bytes, spare size used 64 bytes
NAND flash device: ESMT, id 0xc8d1 block 128KB size 131072KB
Board IP address                  : 192.168.1.1:ffffff00
Host IP address                   : 192.168.1.100
Gateway IP address                :
Run from flash/host/tftp (f/h/c)  : f
Default host run file name        : vmlinux
Default host flash file name      : bcm963xx_fs_kernel
Boot delay (0-9 seconds)          : 3
Boot image (0=latest, 1=previous) : 0
Default host ramdisk file name    :
Default ramdisk store address     :
Board Id (0-29)                   : 963168XF
Number of MAC Addresses (1-32)    : 11
Base MAC Address                  : c5:05:c0:99:70:01
PSI Size (1-64) KBytes            : 24
Enable Backup PSI [0|1]           : 0
System Log Size (0-256) KBytes    : 0
Auxillary File System Size Percent: 0
Main Thread Number [0|1]          : 0

*** Press 't' to stop auto run (0.3 seconds) ***
Booting from latest image (address 0xb9d80000, flash offset 0x01d80000) ...
Decompression OK!
Entry at 0x80402740
Starting program at 0x80402740
Linux version 3.4.11-rt19 (root@tplink) (gcc version 4.6.2 (Buildroot 2011.11) ) #18 SMP PREEMPT Sat May 16 17:21:01 CST 2020

963168XF prom init

CPU revision is: 0002a080 (Broadcom BMIPS4350)

DSL SDRAM reserved: 0x132000

Determined physical RAM map:

memory: 03ece000 @ 00000000 (usable)

Zone PFN ranges:

  DMA      0x00000000 -> 0x00001000

  Normal   0x00001000 -> 0x00003ece

Movable zone start PFN for each node

Early memory PFN ranges

    0: 0x00000000 -> 0x00003ece

On node 0 totalpages: 16078

free_area_init_node: node 0, pgdat 80515e40, node_mem_map 81000000

  DMA zone: 32 pages used for memmap

  DMA zone: 0 pages reserved

  DMA zone: 4064 pages, LIFO batch:0

  Normal zone: 94 pages used for memmap

  Normal zone: 11888 pages, LIFO batch:1

PERCPU: Embedded 7 pages/cpu @81083000 s5488 r8192 d14992 u32768

pcpu-alloc: s5488 r8192 d14992 u32768 alloc=8*4096

pcpu-alloc: [0] 0 [0] 1

Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 15952

Kernel command line: ro noinitrd  irqaffinity=0

PID hash table entries: 256 (order: -2, 1024 bytes)

Dentry cache hash table entries: 8192 (order: 3, 32768 bytes)

Inode-cache hash table entries: 4096 (order: 2, 16384 bytes)

Primary instruction cache 64kB, VIPT, 4-way, linesize 16 bytes.

Primary data cache 32kB, 2-way, VIPT, cache aliases, linesize 16 bytes

Memory: 57996k/64312k available (4096k kernel code, 6316k reserved, 1049k data, 216k init, 0k highmem)

Preemptible hierarchical RCU implementation.

NR_IRQS:128

console [ttyS0] enabled

Calibrating delay loop... 397.31 BogoMIPS (lpj=198656)

pid_max: default: 32768 minimum: 301

Mount-cache hash table entries: 512

--Kernel Config--

  SMP=1

  PREEMPT=1

  DEBUG_SPINLOCK=0

  DEBUG_MUTEXES=0

Broadcom Logger v0.1 May 16 2020 17:15:59

CPU revision is: 0002a080 (Broadcom BMIPS4350)

Primary instruction cache 64kB, VIPT, 4-way, linesize 16 bytes.

Primary data cache 32kB, 2-way, VIPT, cache aliases, linesize 16 bytes

Brought up 2 CPUs

NET: Registered protocol family 16

registering PCI controller with io_map_base unset

registering PCI controller with io_map_base unset

bio: create slab <bio-0> at 0

SCSI subsystem initialized

usbcore: registered new interface driver usbfs

usbcore: registered new interface driver hub

usbcore: registered new device driver usb

PCI host bridge to bus 0000:00

pci_bus 0000:00: root bus resource [mem 0xa0f00000-0xa0ffffff]

pci_bus 0000:00: root bus resource [io  0xa2000000-0xa200ffff]

pci 0000:00:00.0: [14e4:435f] type 00 class 0x028000

pci 0000:00:00.0: reg 10: [mem 0x10004000-0x10005fff]

pci 0000:00:09.0: [14e4:6300] type 00 class 0x0c0310

pci 0000:00:09.0: reg 10: [mem 0x10002600-0x100026ff]

pci 0000:00:0a.0: [14e4:6300] type 00 class 0x0c0320

pci 0000:00:0a.0: reg 10: [mem 0x10002500-0x100025ff]

PCI host bridge to bus 0000:01

pci_bus 0000:01: root bus resource [mem 0x11000000-0x11efffff]

pci_bus 0000:01: root bus resource [??? 0x00000000 flags 0x0]

pci 0000:01:00.0: [14e4:6326] type 01 class 0x060400

pci 0000:01:00.0: PME# supported from D0 D3hot

pci 0000:01:00.0: PCI bridge to [bus 02-02]

bcmhs_spi bcmhs_spi.1: master is unqueued, this is deprecated

bcmleg_spi bcmleg_spi.0: master is unqueued, this is deprecated

skbFreeTask created successfully

[0;34mBLOG v3.0 Initialized[0m

BLOG Rule v1.0 Initialized

Broadcom IQoS v0.1 May 16 2020 17:19:17 initialized

NET: Registered protocol family 8

NET: Registered protocol family 20

Switching to clocksource MIPS

NET: Registered protocol family 2

IP route cache hash table entries: 1024 (order: 0, 4096 bytes)

TCP established hash table entries: 2048 (order: 2, 16384 bytes)

TCP bind hash table entries: 2048 (order: 2, 16384 bytes)

TCP: Hash tables configured (established 2048 bind 2048)

TCP: reno registered

UDP hash table entries: 128 (order: 0, 4096 bytes)

UDP-Lite hash table entries: 128 (order: 0, 4096 bytes)

NET: Registered protocol family 1

PCI: CLS mismatch (64 != 16), using 16 bytes

bcm_tstamp initialized, (hpt_freq=200000000 2us_div=200 2ns_mult=5 2ns_shift=0)

exFAT: Version 1.2.9

jffs2: version 2.2. (NAND) © 2001-2006 Red Hat, Inc.

fuse init (API version 7.18)

msgmni has been set to 113

io scheduler noop registered (default)

Broadcom NAND controller (BrcmNand Controller)

mtd->oobsize=0, mtd->eccOobSize=0

NAND_CS_NAND_XOR=00000000

B4: NandSelect=40000001, nandConfig=15142200, chipSelect=0

brcmnand_read_id: CS0: dev_id=c8d18095

After: NandSelect=40000001, nandConfig=15142200

DevId c8d18095 may not be supported.  Will use config info

Spare Area Size = 16B/512B

Block size=00020000, erase shift=17

NAND Config: Reg=15142200, chipSize=128 MB, blockSize=128K, erase_shift=11

busWidth=1, pageSize=2048B, page_shift=11, page_mask=000007ff

timing1 not adjusted: 6574845b

timing2 not adjusted: 00001e96

ECC level changed to 15

OOB size changed to 16

BrcmNAND mfg 0 0 UNSUPPORTED NAND CHIP 128MB on CS0


Found NAND on CS0: ACC=f7ff1010, cfg=15142200, flashId=c8d18095, tim1=6574845b, tim2=00001e96

BrcmNAND version = 0x0400 128MB @00000000

brcmnand_scan: B4 nand_select = 40000001

brcmnand_scan: After nand_select = 40000001

page_shift=11, bbt_erase_shift=17, chip_shift=27, phys_erase_shift=17

Brcm NAND controller version = 4.0 NAND flash size 128MB @18000000

ECC layout=brcmnand_oob_64

brcmnand_scan:  mtd->oobsize=64

brcmnand_scan: oobavail=50, eccsize=512, writesize=2048

brcmnand_scan, eccsize=512, writesize=2048, eccsteps=4, ecclevel=15, eccbytes=3

-->brcmnand_default_bbt

brcmnand_default_bbt: bbt_td = bbt_main_descr

Bad block table Bbt0 found at page 0000ffc0, version 0x01 for chip on CS0

Bad block table 1tbB found at page 0000ff80, version 0x01 for chip on CS0

brcmnandCET: Status -> Loaded

Creating 6 MTD partitions on "brcmnand.0":

0x000001d80000-0x000003ae0000 : "rootfs"

0x000000020000-0x000001d80000 : "rootfs_update"

0x000003b00000-0x000003f00000 : "data"

0x000000000000-0x000000020000 : "nvram"

0x000001d80000-0x000003ae0000 : "image"

0x000000020000-0x000001d80000 : "image_update"

PPP generic driver version 2.4.2

NET: Registered protocol family 24

usbcore: registered new interface driver usblp

brcmboard: brcm_board_init entry

WIFI: Button Interrupt 0x3 is enabled

RESET: Button Interrupt 0x0 is enabled

SES: Button Interrupt 0x1 is enabled

SES: LED GPIO 0x8016 is enabled

DYING GASP IRQ initialized

Register flash device: flash0

Serial: BCM63XX driver $Revision: 3.00 $

[0;33mMagic SysRq with Auxilliary trigger char enabled (type ^ h for list of supported commands)[0m

ttyS0 at MMIO 0xb0000180 (irq = 13) is a BCM63XX

ttyS1 at MMIO 0xb00001a0 (irq = 42) is a BCM63XX

bcmPktDmaBds_init: Broadcom Packet DMA BDs initialized


GACT probability NOT on

Mirror/redirect action on

u32 classifier

    input device check on

    Actions configured

Netfilter messages via NETLINK v0.30.

nf_conntrack version 0.5.0 (906 buckets, 5120 max)

gre: GRE over IPv4 demultiplexor driver

ip_gre: GRE over IPv4 tunneling driver

ip_tables: (C) 2000-2006 Netfilter Core Team

TCP: cubic registered

Initializing XFRM netlink socket

NET: Registered protocol family 10

ip6_tables: (C) 2000-2006 Netfilter Core Team

IPv6 over IPv4 tunneling driver

NET: Registered protocol family 17

NET: Registered protocol family 15

Ebtables v2.0 registered

ebt_ftos registered

ebt_wmm_mark registered

8021q: 802.1Q VLAN Support v1.8

VFS: Mounted root (jffs2 filesystem) readonly on device 31:0.

Freeing unused kernel memory: 216k freed


starting pid 244, tty '': '/etc/init.d/rcS'
L2TP core driver, V2.0

PPPoL2TP kernel driver, V2.0

chipinfo: module license 'proprietary' taints kernel.

Disabling lock debugging due to kernel taint

brcmchipinfo: brcm_chipinfo_init entry

bcmxtmrt: Broadcom BCM3168D0 ATM/PTM Network Device v0.6 May 16 2020 17:23:40

Broadcom Ingress QoS Module  Char Driver v0.1 May 16 2020 17:21:50 Registered<243>[0m


Broadcom Ingress QoS ver 0.1 initialized

NBUFF v1.0 Initialized

[0;36;44mInitialized fcache state[0m

[0;36;44mBroadcom Packet Flow Cache  Char Driver v2.2 May 16 2020 17:21:51 Registered<242>[0m

Created Proc FS /procfs/fcache

[0;36;44mBroadcom Packet Flow Cache registered with netdev chain[0m

[0;36;44mBroadcom Packet Flow Cache learning via BLOG enabled.[0m

[0;35m[FHW]  pktDbgLvl[0xc00d75e0]=0[0m

[0;34m[FHW]  fhw_construct: [0m

[0;36;44mInitialized Fcache HW accelerator layer state[0m

flwStatsThread created

[0;36;44mConstructed Broadcom Packet Flow Cache v2.2 May 16 2020 17:21:51[0m

bcmxtmcfg: bcmxtmcfg_init entry

adsl: adsl_init entry

Broadcom BCM63168D0 Ethernet Network Device v0.1 May 16 2020 17:23:34

ETH Init: Ch:0 - 200 tx BDs at 0xa30fb000

ETH Init: Ch:1 - 200 tx BDs at 0xa30fa000

ETH Init: Ch:0 - 600 rx BDs at 0xa30e2000

ETH Init: Ch:1 - 100 rx BDs at 0xa3025800

dgasp: kerSysRegisterDyingGaspHandler: bcmsw registered

eth0.2: <Int sw port: 0> <Logical : 00> PHY_ID <0x00000001 : 0x01> MAC : 98:DE:D0:7C:D3:10

eth0.3: <Int sw port: 1> <Logical : 01> PHY_ID <0x00000002 : 0x02> MAC : 98:DE:D0:7C:D3:10

eth0.4: <Int sw port: 2> <Logical : 02> PHY_ID <0x00000003 : 0x03> MAC : 98:DE:D0:7C:D3:10

eth1: <Int sw port: 3> <Logical : 03> PHY_ID <0x00000044 : 0x04> MAC : 98:DE:D0:7C:D3:10

eth0.5: <Int sw port: 4> <Logical : 04> PHY_ID <0x00800010 : 0x10> MAC : 98:DE:D0:7C:D3:10

Energy Efficient Ethernet: Disabled

[0;36;44mBroadcom Packet Flow Cache HW acceleration enabled.[0m

[0;34m[NTC arl] arlEnable : Enabled ARL binding to Flow Cache[0m

Broadcom Address Resolution Logic Processor (ARL) Char Driver v0.1 May 16 2020 17:21:50 Registered <245>

Broadcom 802.1Q VLAN Interface, v0.1

ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver

PCI: Enabling device 0000:00:0a.0 (0000 -> 0002)

ehci_hcd 0000:00:0a.0: setting latency timer to 64

ehci_hcd 0000:00:0a.0: EHCI Host Controller

ehci_hcd 0000:00:0a.0: new USB bus registered, assigned bus number 1

ehci_hcd 0000:00:0a.0: Enabling legacy PCI PM

ehci_hcd 0000:00:0a.0: irq 18, io mem 0x10002500

ehci_hcd 0000:00:0a.0: USB f.f started, EHCI 1.00

hub 1-0:1.0: USB hub found

hub 1-0:1.0: 2 ports detected

ohci_hcd: USB 1.1 'Open' Host Controller (OHCI) Driver

PCI: Enabling device 0000:00:09.0 (0000 -> 0002)

ohci_hcd 0000:00:09.0: setting latency timer to 64

ohci_hcd 0000:00:09.0: OHCI Host Controller

ohci_hcd 0000:00:09.0: new USB bus registered, assigned bus number 2

ohci_hcd 0000:00:09.0: irq 17, io mem 0x10002600

hub 2-0:1.0: USB hub found

hub 2-0:1.0: 2 ports detected

Initializing USB Mass Storage driver...

usbcore: registered new interface driver usb-storage

USB Mass Storage support registered.

hub 1-0:1.0: over-current condition on port 2

dns_init

PPP MPPE Compression module registered

PPTP driver version 0.8.5


Please press Enter to activate this console. [ dm_readFile ] 2061:  can not open xml file /var/tmp/pc/reduced_data_model.xml!, about to open file /etc/reduced_data_model.xml
[ initKernelMonitorFd ] 525:  kernelMonitormonitor task is initialized pid= 468

Fd=6

[ initKernelMonitorFd ] 543:  registered fd 6 with kernel monitor

send 2001 error No such file or directory ,pid 353
Success
ioctl: No such device
Generating 2048 bit rsa key, this may take a while...
Generating 1024 bit dss key, this may take a while...
ADDRCONF(NETDEV_UP): eth0.4: link is not ready

device eth0.4 entered promiscuous mode

Success
ADDRCONF(NETDEV_UP): eth0.3: link is not ready

device eth0.3 entered promiscuous mode

igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 90; error = Address already in use
igmpd# Err: setsockopt - MRT_ADD_VIF
Success
ADDRCONF(NETDEV_UP): eth0.2: link is not ready

device eth0.2 entered promiscuous mode

igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 90; error = Address already in use
igmpd# Err: setsockopt - MRT_ADD_VIF
Success
ADDRCONF(NETDEV_UP): eth0.5: link is not ready

device eth0.5 entered promiscuous mode

igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 90; error = Address already in use
igmpd# Err: setsockopt - MRT_ADD_VIF
Success
[DBG:700] ADSL dr*** dslThread dslPid=555

BcmAdsl_Initialize=0xC016C050, g_pFnNotifyCallback=0xC01A5790

iver returns error

[ oal_dsl_isAtmConnection ] 3918:  Failed to freshAdslMibInfo
[DBG:939] ADSL driver returns error

lmemhdr[2]=0x100CE000, pAdslLMem[2]=0x100CE000

pSdramPHY=0xA3FFFFF8, 0x1B77B3 0xDEADBEEF

*** XfaceOffset: 0x5FF90 => 0x5FF90 ***

*** PhySdramSize got adjusted: 0xF7844 => 0x12BD20 ***

AdslCoreSharedMemInit: shareMemSize=25280(25280)

AdslCoreHwReset:  pLocSbSta=83b98000 bkupThreshold=3072

AdslCoreHwReset:  AdslOemDataAddr = 0xA3FB6278

***BcmDiagsMgrRegisterClient: 0 ***

dgasp: kerSysRegisterDyingGaspHandler: dsl0 registered

XTM Init: Ch:0 - 600 rx BDs at 0xa3b96000

XTM Init: Ch:1 - 16 rx BDs at 0xa2c7ae80

bcmxtmrt: PTM/ATM Non-Bonding Mode configured in system

Public key portion is:
ssh-dss AAAAB3NzaC1kc3MAAACBANm1b7x4prfeyZb9ECqOh8zxbf0E+DGwGSpWDUCeo4pfcfQuqGW5vjJ5xwvoUqpxeNLh8Q4WcXPiQ6SAI0eRSGIcdXiFkk7dZzWQK52eKkUbWs8zvIm5tk658MxJscBbIDDUlHeuTW6YRe3J71Vwlt0cP/ZCa7MwACgd+RYaZwezAAAAFQC3qZrUqmN40W5BI2qOzHb/VPIkeQAAAIBxoXOU7DrOvzm/eirtoVo14uymC25MDTHwRVGdaNBH4+uJuFRGxY20BFBK02x7YTJpEkrEZQHhInSrhs8dMJlhH+CbhtDrdu+UavA1dL0Mrf76eplDYfkhlUqoWaktjN8n1Bvc2X6UO6Bd9DK1AoMNnXQpP5K7OKzJc/OoRLqE7gAAAIBOVM7M+c+6jy99QhjfULzTa9W8Yuy1VQdSm+oNzKAevNBum0TS724iX//E5XwnlgawkYkfIVJ2vRFAZopX4S4gN6c9tkrQUYIIWOdG2FzBhhzAIWxjErtkl6+W7bUD543pAxCOWdJ+LL9Ayyp7s5rmOxANT724Opu17PyBQrW8Gg== admin@TD-W9970
Fingerprint: sha1!! 11:f7:02:a0:4a:b0:ea:05:6b:77:7c:1e:06:e6:93:ad:84:d9:8f:91
open DNS error: No such file or directory
[ oal_sys_getOldTZInfo ] 435:  Open TZ file error!
Public key portion is:
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDCud5uZOtwDpyu90LbZ/HkHSQSVYR0p8qqUZauw6GvVvOInb2V+bdH1+1IBPE2mUFFMkoomIitTD0knCKw/8pVCb9mALzh3M/j3s14upZ3KAGO1oxzVmeZIEEwAMAN8NJjjlYZJ0DGii+aPiEDV6r1Q85UIlQnKRHe5wAfA7rM/dmqFSVbvw+1EsJq7ylCQ7UIPri7sb/zDkpGS6DPG0NAs/o1RkwGVe6EXWFqzLrO07qMiHwZZwjviIFRUpF1drLUqGvOGPsdlF5Pjq6ZyL7BAfIER/M7uOhV9EFDkq/5iugceLGN5uxG25lBQ/qvSy+bqDiVuU8does9qETMEauL admin@TD-W9970
Fingerprint: sha1!! b3:f7:4e:d1:f1:5b:39:a2:ff:58:1e:c1:02:71:2e:9b:07:54:9c:57
--SMP support

wl: dsl_tx_pkt_flush_len=338

wl: norm_wmark_tot=400, pktc_wmark_tot=2048

wl 0000:00:00.0: setting latency timer to 64

wl: passivemode=1

wl0: creating kthread wl0-kthrd

wl: napimode=0

Neither SPROM nor OTP has valid image

wl:srom/otp not programmed, using main memory mapped srom info(wombo board)

wl:loading /etc/wlan/bcm6362_map.bin

wl: updating srom from flash...

wl: updating srom from flash...

srom rev:8

wl0: allocskbmode=1 currallocskbsz=256

wl0: Broadcom BCM435f 802.11 Wireless Controller 6.37.14.4803.cpe4.16L01.0-kdb

dgasp: kerSysRegisterDyingGaspHandler: wl0 registered

Setting SSID: "TurkTelekom_TD310"
wlctl: Unsupported
wlctl: Not up
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: scan in progress ...
acsd: selected channel spec: 0x1004
device wl0 entered promiscuous mode

br0: port 5(wl0) entered forwarding state

br0: port 5(wl0) entered forwarding state

igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 123; error = Address already in use
igmpd# Err: setsockopt - MCAST_JOIN_GROUP
igmpd# file: src/igmp_ifinfo.c;line: 90; error = Address already in use
igmpd# Err: setsockopt - MRT_ADD_VIF
brctl: iface wl0.2: No such device
ioctl - SIOCGIFINDEX: No such device
brctl: iface wl0.3: No such device
ioctl - SIOCGIFINDEX: No such device
brctl: iface wl0.4: No such device
ioctl - SIOCGIFINDEX: No such device
[ rsl_initLanWlanObj ] 9542:  if name = wlan1

[ rsl_initLanWlanObj ] 9542:  if name = wlan2

[ rsl_initLanWlanObj ] 9542:  if name = wlan3

send 2030 error No such file or directory ,pid 353
send 2030 error No such file or directory ,pid 353
send 2030 error No such file or directory ,pid 353
send 2030 error No such file or directory ,pid 353
send 2030 error No such file or directory ,pid 353
send 2030 error No such file or directory ,pid 353
send 2030 error No such file or directory ,pid 353
send 2030 error No such file or directory ,pid 353
killall: dnsmasq: no process killed
[ rsl_getManagementServerObj ] 375:  cannot set connectionRequestURL yet because no WAN intf is up
[ rsl_getManagementServerObj ] 375:  cannot set connectionRequestURL yet because no WAN intf is up
[ rsl_getManagementServerObj ] 375:  cannot set connectionRequestURL yet because no WAN intf is up
ip6tables: No chain/target/match by that name.
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
ip6tables: Bad rule (does a matching rule exist in that chain?).
ip6tables: Bad rule (does a matching rule exist in that chain?).
ip6tables: No chain/target/match by that name.
ip6tables: No chain/target/match by that name.
radvd starting
[Jan 01 03:00:44] radvd: no linklocal address configured for br0
[Jan 01 03:00:44] radvd: error parsing or activating the config file: /var/tmp/dconf/radvd_br0.conf
sh: pwrctl: not found
ADDRCONF(NETDEV_UP): eth1: link is not ready

sh: pwrctl: not found
sh: pwrctl: not found
[ rsl_wan_calWanReservedMacFromLanMac ] 1207:  flashmac=98:DE:D0:7C:D3:10
[ rsl_wan_calWanReservedMacFromLanMac ] 1207:  flashmac=98:DE:D0:7C:D3:10
[ rsl_wan_calWanReservedMacFromLanMac ] 1207:  flashmac=98:DE:D0:7C:D3:10
sh: can't create /proc/sys/net/ipv6/conf/ptm0.55/disable_ipv6: nonexistent directory
ifconfig: ioctl 0x8913 failed: No such device
[ rsl_wan_calWanReservedMacFromLanMac ] 1207:  flashmac=98:DE:D0:7C:D3:10
eth1.55 MAC address set to 98:DE:D0:7C:D3:10

netdev path : eth1.55 -> eth1

BCMVLAN : eth1 mode was set to RG

Created new Tag Rule: dev=eth1, dir=1, tags=0, id=0

Created new Tag Rule: dev=eth1, dir=0, tags=0, id=0

Created new Tag Rule: dev=eth1, dir=0, tags=1, id=0

Created new Tag Rule: dev=eth1, dir=0, tags=2, id=0

Created new Tag Rule: dev=eth1, dir=0, tags=1, id=1

Created new Tag Rule: dev=eth1, dir=0, tags=2, id=1

eth1.55 MAC address set to 98:DE:D0:7C:D3:11

device eth1 entered promiscuous mode

[ rsl_wan_calWanReservedMacFromLanMac ] 1207:  flashmac=98:DE:D0:7C:D3:10
sh: can't create /proc/sys/net/ipv6/conf/ptm0.35/disable_ipv6: nonexistent directory
ifconfig: ioctl 0x8913 failed: No such device
[ wan_conn_pppoeConn ] 089:  L2 interface not exist(up), don't start pppd!
[ rsl_wan_calWanReservedMacFromLanMac ] 1207:  flashmac=98:DE:D0:7C:D3:10
eth1.35 MAC address set to 98:DE:D0:7C:D3:10

netdev path : eth1.35 -> eth1

BCMVLAN : eth1 mode was set to RG

Created new Tag Rule: dev=eth1, dir=1, tags=0, id=1

Created new Tag Rule: dev=eth1, dir=0, tags=0, id=1

Created new Tag Rule: dev=eth1, dir=0, tags=1, id=2

Created new Tag Rule: dev=eth1, dir=0, tags=2, id=2

Created new Tag Rule: dev=eth1, dir=0, tags=1, id=3

Created new Tag Rule: dev=eth1, dir=0, tags=2, id=3

eth1.35 MAC address set to 98:DE:D0:7C:D3:11

[ getPidFromPidFile ] 112:  Cann't open file: /var/run/zebra.pid.
[ getPidFromPidFile ] 112:  Cann't open file: /var/run/ripd.pid.
[ read_dhcpc_config ] 113: error, unable to open config file: /var/tmp/dconf/udhcpc.conf
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
Sorry, rule does not exist.
ip6tables: Bad rule (does a matching rule exist in that chain?).
ip6tables: Bad rule (does a matching rule exist in that chain?).
ip6tables: Bad rule (does a matching rule exist in that chain?).
[ rsl_setStorageServiceObj ] 1256:  mountFlag is 3,We start usb server

killall: ushare: no process killed
[ cwmp_parseAcsInfo ] 1235:  No available connection for hostGetByName
uShare (version 1.1a), a lightweight UPnP A/V and DLNA Media Server.
Benjamin Zores (C) 2005-2007, for GeeXboX Team.
See http://ushare.geexbox.org/ for updates.
iptables: Bad rule (does a matching rule exist in that chain?).
iptables: Bad rule (does a matching rule exist in that chain?).
[ dm_getObjNode ] 762:  Object(oid = 0)'s infomation is not exist.
[ dm_getObj ] 660:  Get object information failed. object oid = 0
[ generalInitPageAttribute ] 2088:  Get object for oid 0 error, ret = 9804
open DNS error: No such file or directory
[ cwmp_parseAcsInfo ] 1235:  No available connection for hostGetByName


starting pid 354, tty '': '/sbin/getty -L ttyS0 115200 vt100'


TD-W9970 login: root
Password:
Jan  1 03:01:27 login[354]: root login on 'console'

~ #
```
