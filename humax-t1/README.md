## Humax T1
![ProductList_tr_t1](https://github.com/onerc/reverse-engineering/assets/94126150/0a19e131-81b4-47ff-a95f-692690818d49)

Yet another sketchy baby/"security"/IP camera

[Product page](https://tr.humaxdigital.com/product/t1/)

## Port scanning
![1637446355761](https://github.com/onerc/reverse-engineering/assets/94126150/e059ab1c-2332-43cf-8b99-02cada17ad3c)

Telnet is on by default, credentials are `root:hslwificam`.

## Web UI
![1637446573944](https://github.com/onerc/reverse-engineering/assets/94126150/20fc1c26-47eb-421f-8a66-0ad9133052dc)

No password for user `admin` by default.

## Internals
![humax](https://github.com/onerc/reverse-engineering/assets/94126150/da3d94ce-2a4c-456d-9b39-ecde765383ec)

At least they were kind enough to label the pins. Or too lazy to remove them.

## Boot log
<details>

```
U-Boot 2010.06 (Jul 15 2015 - 13:47:23)

Check spi flash controller v350... Found
Spi(cs1) ID: 0xC2 0x20 0x17 0xC2 0x20 0x17
Spi(cs1): Block:64KB Chip:8MB Name:"MX25L6406E"
In:    serial
Out:   serial
Err:   serial
motobooton=0 leveltimes=5250 vertimes=1300 delay=500000 speedmode=200 runtimes=75
gpio1_7 value -10
Hit any key to stop autoboot:  0
8192 KiB hi_sfc at 0:0 is now current device

## Booting kernel from Legacy Image at 82000000 ...
   Image Name:   Linux-3.0.8
   Image Type:   ARM Linux Kernel Image (uncompressed)
   Data Size:    1444004 Bytes = 1.4 MiB
   Load Address: 80008000
   Entry Point:  80008000
   Loading Kernel Image ... OK
OK

Starting kernel ...

Uncompressing Linux... done, booting the kernel.
Linux version 3.0.8 (root@ubuntu) (gcc version 4.4.1 (Hisilicon_v100(gcc4.4-290+uclibc_4
CPU: ARM926EJ-S [41069265] revision 5 (ARMv5TEJ), cr=00053177
CPU: VIVT data cache, VIVT instruction cache
Machine: hi3518
Memory policy: ECC disabled, Data cache writeback
AXI bus clock 200000000.
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 9144
Kernel command line: mem=36M console=ttyAMA0,115200 root=/dev/mtdblock2 rootfstype=squa)
PID hash table entries: 256 (order: -2, 1024 bytes)
Dentry cache hash table entries: 8192 (order: 3, 32768 bytes)
Inode-cache hash table entries: 4096 (order: 2, 16384 bytes)
Memory: 36MB = 36MB total
Memory: 32904k/32904k available, 3960k reserved, 0K highmem
Virtual kernel memory layout:
    vector  : 0xffff0000 - 0xffff1000   (   4 kB)
    fixmap  : 0xfff00000 - 0xfffe0000   ( 896 kB)
    DMA     : 0xffc00000 - 0xffe00000   (   2 MB)
    vmalloc : 0xc2800000 - 0xfe000000   ( 952 MB)
    lowmem  : 0xc0000000 - 0xc2400000   (  36 MB)
    modules : 0xbf000000 - 0xc0000000   (  16 MB)
      .init : 0xc0008000 - 0xc001f000   (  92 kB)
      .text : 0xc001f000 - 0xc035d000   (3320 kB)
      .data : 0xc035e000 - 0xc0372ca0   (  84 kB)
       .bss : 0xc0372cc4 - 0xc037fed0   (  53 kB)
SLUB: Genslabs=13, HWalign=32, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
NR_IRQS:32 nr_irqs:32 32
sched_clock: 32 bits at 100MHz, resolution 10ns, wraps every 42949ms
Calibrating delay loop... 218.72 BogoMIPS (lpj=1093632)
pid_max: default: 32768 minimum: 301
Mount-cache hash table entries: 512
CPU: Testing write buffer coherency: ok
NET: Registered protocol family 16
Serial: AMBA PL011 UART driver
uart:0: ttyAMA0 at MMIO 0x20080000 (irq = 5) is a PL011 rev2
console [ttyAMA0] enabled
uart:1: ttyAMA1 at MMIO 0x20090000 (irq = 5) is a PL011 rev2
bio: create slab <bio-0> at 0
SCSI subsystem initialized
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
cfg80211: Calling CRDA to update world regulatory domain
Switching to clocksource timer1
NET: Registered protocol family 2
IP route cache hash table entries: 1024 (order: 0, 4096 bytes)
TCP established hash table entries: 2048 (order: 2, 16384 bytes)
TCP bind hash table entries: 2048 (order: 1, 8192 bytes)
TCP: Hash tables configured (established 2048 bind 2048)
TCP reno registered
UDP hash table entries: 256 (order: 0, 4096 bytes)
UDP-Lite hash table entries: 256 (order: 0, 4096 bytes)
NET: Registered protocol family 1
squashfs: version 4.0 (2009/01/31) Phillip Lougher
JFFS2 version 2.2. (NAND) © 2001-2006 Red Hat, Inc.
fuse init (API version 7.16)
msgmni has been set to 64
Block layer SCSI generic (bsg) driver version 0.4 loaded (major 254)
io scheduler noop registered
io scheduler deadline registered (default)
io scheduler cfq registered
brd: module loaded
Spi id table Version 1.22
Spi(cs1) ID: 0xC2 0x20 0x17 0xC2 0x20 0x17
SPI FLASH start_up_mode is 3 Bytes
Spi(cs1):
Block:64KB
Chip:8MB
Name:"MX25L6406E"
spi size: 8MB
chip num: 1
4 cmdlinepart partitions found on MTD device hi_sfc
Creating 4 MTD partitions on "hi_sfc":
0x000000000000-0x000000040000 : "boot"
0x000000040000-0x0000001b0000 : "kernel"
0x0000001b0000-0x000000530000 : "rootfs"
0x000000530000-0x000000800000 : "system"
Fixed MDIO Bus: probed
himii: probed
usbcore: registered new interface driver rt2500usb
usbcore: registered new interface driver rt73usb
usbmon: debugfs is not available
ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
hiusb-ehci hiusb-ehci.0: HIUSB EHCI
hiusb-ehci hiusb-ehci.0: new USB bus registered, assigned bus number 1
hiusb-ehci hiusb-ehci.0: irq 15, io mem 0x100b0000
hiusb-ehci hiusb-ehci.0: USB 0.0 started, EHCI 1.00
hub 1-0:1.0: USB hub found
hub 1-0:1.0: 1 port detected
ohci_hcd: USB 1.1 'Open' Host Controller (OHCI) Driver
hiusb-ohci hiusb-ohci.0: HIUSB OHCI
hiusb-ohci hiusb-ohci.0: new USB bus registered, assigned bus number 2
hiusb-ohci hiusb-ohci.0: irq 16, io mem 0x100a0000
hub 2-0:1.0: USB hub found
hub 2-0:1.0: 1 port detected
TCP cubic registered
Initializing XFRM netlink socket
NET: Registered protocol family 17
NET: Registered protocol family 15
lib80211: common routines for IEEE802.11 drivers
registered taskstats version 1
VFS: Mounted root (squashfs filesystem) readonly on device 31:2.
Freeing init memory: 92K
usb 1-1: new high speed USB device number 2 using hiusb-ehci

    __  _______                      __  __    _       __
   / / / / ___/____ ___  ____ ______/ /_/ /   (_)___  / /__
  / /_/ /\__ \/ __ `__ \/ __ `/ ___/ __/ /   / / __ \/ //_/
 / __  /___/ / / / / / / /_/ / /  / /_/ /___/ / / / / ,<
/_/ /_//____/_/ /_/ /_/\__,_/_/   \__/_____/_/_/ /_/_/|_|

[RCS]: /etc/init.d/S00devs
[RCS]: /etc/init.d/S01udev
udevd (299): /proc/299/oom_adj is deprecated, please use /proc/299/oom_score_adj instea.
[RCS]: /etc/init.d/S80network
Empty flash at 0x000d20c0 ends at 0x000d2500
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2500: 0x7401 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2504: 0x0051 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2508: 0x0404 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d250c: 0x4143 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2510: 0x3431 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2514: 0x3834 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2518: 0x0f20 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d251c: 0x3007 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2520: 0x3433 instead
jffs2_scan_eraseblock(): Magic bitmask 0x1985 not found at 0x000d2524: 0x3837 instead
Further such events for this erase block will not be printed
Hisilicon Watchdog Timer: 0.01 initialized. default_margin=60 sec (nowayout= 0, nodeamo)

(none) login: ifconfig: ra0: error fetching interface information: Device not found
not find mac===Get wifi ap mac:===
ifconfig: ra0: error fetching interface information: Device not found
not find mac===Get wifi mac:===
sscanf return 6
@@@@ APSSID APCAM_14F448 @@@@
insmod /lib/modules/wifi/mtutil7601Usta.ko
insmod /lib/modules/wifi/mt7601Usta.ko
mt7601Usta: module license 'unspecified' taints kernel.
Disabling lock debugging due to kernel taint
insmod /lib/modules/wifi/mtnet7601Usta.ko
rtusb init rtusbSTA --->


=== pAd = c2ae9000, size = 860440 ===

<-- RTMPAllocTxRxRingMemory, Status=0
<-- RTMPAllocAdapterBlock, Status=0
RTMP_COM_IoctlHandle():pAd->BulkOutEpAddr=0x8
RTMP_COM_IoctlHandle():pAd->BulkOutEpAddr=0x4
RTMP_COM_IoctlHandle():pAd->BulkOutEpAddr=0x5
RTMP_COM_IoctlHandle():pAd->BulkOutEpAddr=0x6
RTMP_COM_IoctlHandle():pAd->BulkOutEpAddr=0x7
RTMP_COM_IoctlHandle():pAd->BulkOutEpAddr=0x9
NVM is EFUSE
Endpoint(8) is for In-band Command
Endpoint(4) is for WMM0 AC0
Endpoint(5) is for WMM0 AC1
Endpoint(6) is for WMM0 AC2
Endpoint(7) is for WMM0 AC3
Endpoint(9) is for WMM1 AC0
Endpoint(84) is for Data-In
Endpoint(85) is for Command Rsp
usbcore: registered new interface driver rtusbSTA
===Get wifi ap mac:00:00:00:00:00:00===
===Get wifi mac:00:00:00:00:00:00===
SysParamRead system.ini
RTSP Port 10554
ONVIF Port 10080
SysLanguageRead language.ini
Now Language is English !
/usr/bin/unzip -o /system/system/bin/audio_en.zip -d /tmp
user0: pwd:
user1: pwd:
user2:admin pwd:
user0: pwd:
user1: pwd:
user2:admin pwd:
sysversion:R35.9.9.1.18E
SysParamRead factory.ini
ssid: mode 0 wifiauth 0 wifikey:
route: SIOCDELRT: No such process
1. LDO_CTR0(6c) = a64799, PMU_OCLEVEL c
2. LDO_CTR0(6c) = a6478d, PMU_OCLEVEL 6
FW Version:0.1.00 Build:7640
Build Time:201308222153____
ILM Length = 47000(bytes)
DLM Length = 0(bytes)
Loading FW....
#
RTMP_TimerListAdd: add timer obj c2b6992c!
RTMP_TimerListAdd: add timer obj c2b69944!
RTMP_TimerListAdd: add timer obj c2b6995c!
RTMP_TimerListAdd: add timer obj c2b69914!
RTMP_TimerListAdd: add timer obj c2b698cc!
RTMP_TimerListAdd: add timer obj c2b698e4!
RTMP_TimerListAdd: add timer obj c2afe764!
RTMP_TimerListAdd: add timer obj c2aeb1e0!
RTMP_TimerListAdd: add timer obj c2aeb1fc!
RTMP_TimerListAdd: add timer obj c2afe7bc!
RTMP_TimerListAdd: add timer obj c2aedcf0!
RTMP_TimerListAdd: add timer obj c2aed3a0!
RTMP_TimerListAdd: add timer obj c2aedcd4!
RTMP_TimerListAdd: add timer obj c2aedf14!
RTMP_TimerListAdd: add timer obj c2aedd0c!
RTMP_TimerListAdd: add timer obj c2aedd28!
RTMP_TimerListAdd: add timer obj c2aedd44!
RTMP_TimerListAdd: add timer obj c2afe734!
RTMP_TimerListAdd: add timer obj c2afe7a4!
RTMP_TimerListAdd: add timer obj c2aedf44!
RTMP_TimerListAdd: add timer obj c2aedf5c!
RTMP_TimerListAdd: add timer obj c2aedf74!
RTMP_TimerListAdd: add timer obj c2aedf8c!
cfg_mode=9
wmode_band_equal(): Band Equal!
Key2Str is Invalid key length(0) or Type(0)
Key3Str is Invalid key length(0) or Type(0)
Key4Str is Invalid key length(0) or Type(0)
1. Phy Mode = 14
2. Phy Mode = 14
NVM is Efuse and its size =1d[1e0-1fc]
3. Phy Mode = 14
AntCfgInit: primary/secondary ant 0/1
---> InitFrequencyCalibration
InitFrequencyCalibrationMode:Unknow mode = 3
InitFrequencyCalibration: frequency offset in the EEPROM = 105(0x69)
<--- InitFrequencyCalibration
MCS Set = ff 00 00 00 01
<==== rt28xx_init, Status=0
0x1300 = 00064300
RTMPDrvOpen(1):Check if PDMA is idle!
RTMPDrvOpen(2):Check if PDMA is idle!
========mac=00:02:B2:14:F4:48===========
route: SIOCDELRT: No such process
dns1:8.8.8.8 dns2:192.168.1.105
val_out 1409
val_in 7
val_out 0
val_in 10
===IpcSocketInit=6666===
===IpcSocketInit end=3===
===snetworkethmac:00:02:B2:14:F4:48  snetworkwifimac:00:00:00:00:00:00===
 SearchAppInit by zxh
ServiceInit by zxh
IPCUpdateProc 1
start app update thread
update Socket proc is start
update socket init
===SearchThreadProc===
===wificam is start===
0x20050000 value is 0x150124
load hi3518e mpp ko for mii
Hisilicon Media Memory Zone Manager
Hisilicon UMAP device driver interface: v3.00
pa:82400000, va:c2c40000
load sys.ko ...OK!
load viu.ko ...OK!
ISP Mod init!
load vpss.ko ....OK!
load venc.ko ...OK!
load group.ko ...OK!
load chnl.ko ...OK!
load h264e.ko ...OK!
load jpege.ko ...OK!
load rc.ko ...OK!
load region.ko ....OK!
load vda.ko ....OK!
*************************init down!
hi_i2c init is ok!
Kernel: ssp initial ok!
acodec inited!
GpioDataGpioMux:0
GpioDataGpioDir:0
GpioMotoInit
===EncryptCheckOk===
===Get wifi ap mac:48:02:2A:20:81:05===
===Get wifi mac:48:02:2A:20:81:05===
===write data c0 ack 1===
===check chip 1->error 0->ok ===1
===Get wifi ap mac:48:02:2A:20:81:05===
===Get wifi mac:48:02:2A:20:81:05===
SysParamRead system.ini
RTSP Port 10554
ONVIF Port 10080
SysLanguageRead language.ini
Now Language is English !
/usr/bin/unzip -o /system/system/bin/audio_en.zip -d /tmp
user0: pwd:
user1: pwd:
user2:admin pwd:
user0: pwd:
user1: pwd:
user2:admin pwd:
sysversion:R35.9.9.1.18E
SysParamRead factory.ini
===Get wifi ap mac:48:02:2A:20:81:05===
===Get wifi mac:48:02:2A:20:81:05===
sscanf return 6
@@@@ APSSID APCAM_14F448 @@@@
===RtcInit===
3AlarmTimerParamRead 4 0-0-0-0
##Waiting for codec init done!
##Waiting for codec init done!
===H264ParamInit===
H264ParamInit bright 128 hue 128 saturation 128 contrast 128 videomode 0 videoenv 0 bit0
===H264StreamInit===
===InitVideoEncoder===
sensor list num 5
ov9712 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0x9711
OV9760 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0x9760
gc1004 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0x1004
ar0130 id = 0xffff
sensor_list id = 0xffff , ID = 0x2402
soih42 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0xa042
id = 0x0

gVdaWndWidth 40 gVdaWndHeight 22
MPP Version  HI_VERSION=Hi3518_MPP_V1.0.0.0
sensor list num 5
ov9712 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0x9711
OV9760 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0x9760
gc1004 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0x1004
ar0130 id = 0xffff
sensor_list id = 0xffff , ID = 0x2402
soih42 idl = 0xff idh = 0xff
sensor_list id = 0xffff , ID = 0xa042
id = 0x0

+++++++++++++++++++++sensorid:0,/system/system/lib/libsns_ov9712_plus.so
==sensor_register_callback===
===sensorid=0===





############## SetAntiFlickerFrequency,restart:1,fre:50
##Waiting for codec init done!
===ISP_Run===0===
===HI_MPI_ISP_SetImageAttr===25===
aplink ISP_AI = 0 ------------------------------------------------------
HI_MPI_VI_SetChnAttr 0
gMppCfg.gMaxRes = 0
InitNormalVpss
===InitVideoVpss===
===InitVideoEncoder end===
===H264 osd init===
File size = 261702
netok 246 link 0
wifi dhcp return -1
===StartVideoEncoder for 720P===ratemode=0 framerate=15 bitrate=1024
VpssGrp 0 VpssChn 0 VencGrp 0 VencChn 0 enSize 16
stPicSize.u32Width=1280 stPicSize.u32Height=720
===StartVideoEncoder for VGA===
VpssGrp 0 VpssChn 1 VencGrp 1 VencChn 1 enSize 7
stPicSize.u32Width=640 stPicSize.u32Height=360
===StartVideoEncoder for QVGA===
VpssGrp 0 VpssChn 3 VencGrp 2 VencChn 2 enSize 6
stPicSize.u32Width=320 stPicSize.u32Height=180


GetAVStreamInOneChn Start!!

================ CreateSnapChn:170 success
HI_MPI_RGN_GetDisplayAttr (1)) failed with 0xa0128005!
===ShowVideoOsd_Time===
===ShowVideoOsd===
channelname------------------:WIFICAM


GetAVStreamInOneChn Start!!



GetAVStreamInOneChn Start!!



JpegSnapProcess Start!!

===ShowbitrateOsd===
===StartOsdProcess===
===H264SoftWdtThread====
===H264SetParam===
contrast 50 hue 50 luma 50 satu 50
contrast 50 hue 50 luma 50 satu 50
contrast 50 hue 50 luma 50 satu 50
contrast 50 hue 50 luma 50 satu 50
VideoMirrorFlipSet0=4
VideoMirrorFlipSet1
VideoMirrorFlipSet2
H264SetBitRate channel 0 ratemode 0 bybitrate 1024
VideoSetBitRate channel 0 rcmode 13 ratemode 0 vbrrate 1024 cbrbitrate 1024
u32MinIprop 1 u32MaxIprop 4 s32IPQPDelta 6
H264SetBitRate channel 1 ratemode 1 bybitrate 512
VideoSetBitRate channel 1 rcmode 14 ratemode 1 vbrrate 512 cbrbitrate 512
u32MinIprop 1 u32MaxIprop 4 s32DeltaQP 6
H264SetBitRate channel 2 ratemode 0 bybitrate 128
VideoSetBitRate channel 2 rcmode 13 ratemode 0 vbrrate 256 cbrbitrate 256
u32MinIprop 1 u32MaxIprop 4 s32IPQPDelta 6
===H264SetParam end===
HI_MPI_ISP_GetAWBAlgType:1 iRet 0
HI_MPI_ISP_SetAWBAlgType:1 iRet 0
sensorid = 0
use gamma1
OV9712 gamma table index 1
StreamLiveProc 0
StreamLiveProc 3
StreamLiveProc 2
StreamLiveProc 1
===audio Codec Init===0
===AudioHwInit===
InitAudio: InitAudioInitAudio,/dev/acodec
===StartAudioEncode===
StreamRecordProc 0
StreamRecordProc 1
StreamRecordProc 2
StreamRecordProc 3
StreamVideoProc 0
StreamVideoProc 1
StreamVideoProc 3
StreamVideoProc 2
Get ISP Interrupt Failed with ec 0x1!
SetAudioDevADGain: InitAudioInitAudio,/dev/acodec
Waite Dev Start OK ! AiFd = 31
Get ISP Interrupt Failed with ec 0x1!
StartAudioDecode Success
SetInPutVolume :24
SetOutPutVolume :24
1AlarmTimerParamRead 1 0-0-0-0
2AlarmTimerParamRead 2 0-0-0-0
p2pdeviceid:HSL-367545-VHWKF
PLAY_AUDIO_TASK createthread
AudioPlayProc:392
start motion check
===MotionDetectionInit=0===
MotionDetectionUserCfg enable 0 sentive 0
start sound check
start alarm timer check
========version:1050101===========
apklink iRet 7
HSL iRet 0
select venc :0 time out!!!
select venc :1 time out!!!
select venc :2 time out!!!
Waite Dev Start OK ! AiFd = 31
Get ISP Interrupt Failed with ec 0x1!
===StartMotionDetection===
MDThreadBody is start...36
Waite Dev Start OK ! AiFd = 31
Get ISP Interrupt Failed with ec 0x1!
sensorid = 0
use gamma1
OV9712 gamma table index 1
ircut is switch off
select venc :0 time out!!!
select venc :1 time out!!!
select venc :2 time out!!!
netok 246 link 0
wifi dhcp return -1
Waite Dev Start OK ! AiFd = 31
```
</details>
