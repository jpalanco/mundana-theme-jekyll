---
title: "IoT Reversing 101: Discovery"
date: "2020-8-9"
image: assets/images/iotreversing.jpeg
author: name
layout: post
tags: [ IoT, reversing, discovery ]
categories: [ reverse engineering ]
---


Before we delve into the world of reverse engineering, we need to discuss what engineering as a whole actually is.

Engineering is the science of making things.

This includes defining the product requirements, designing the product and building or manufacturing the product as a whole.

Reverse engineering is the engineering process done in reverse with a limited scope.

A limited scope project is the understanding of how to modify the router firmware to add features and additional programs.

## The Information Gathering Process

Before we begin the reverse engineering process, we need to figure out a few things about the device, this process is known as information gathering.

Who makes the devices and is there an original design manufacturer for the device?

To do this, simply start by opening the case and identifying the main device components.

Locate the UART and JTAG interfaces and get the firmware and the root file system.

### Locating the UART interface

You can start by searching on the internet and identifying potential serial headers candidates.

These can be marked in the PCB’s silkscreen and are usually 4 pins such as VCC, GND, TX and RX.

You can use a multimeter to find the potential candidates and locate pins on the SOC to follow PCB traces.

To do this effectively, use a tool such as a Jtagulator, Oscillioscope or Logic Analyzer to locate the TX.

### Locating the JTAG interface

JTAG is an industry standard for testing printed circuit boards after they are manufactured and as such, allows access to read and write flash memory contents and in turn can be used as a means for an in-circuit emulator.

Multiple devices are daisy-chained together this way.

The pins you need to look for are:

<![if !supportLists]>· <![endif]>TCK test clock

<![if !supportLists]>· <![endif]>TDI test data in

<![if !supportLists]>· <![endif]>TDO test data out

<![if !supportLists]>· <![endif]>TMS test mode sel.

<![if !supportLists]>· <![endif]>TRST test reset.

While there is no standard pinout, there are a pinouts, to find them search on the internet and look for headers labeled TCK, TDI, TDO, TMS.  
You can look for 1x5/6. 2x5, 2x7, 2x10 pin headers.

Make sure to look out for GND and VCC with a multimeter and compare them to the popular pinouts, as often there are pullups between 1 to 100k for TMS, TDI and RTST, TRST can be pulled low.

TDO should be high impedance.

Locate the pins on SOC and follow PCB traces by using a tool such as a Jtagulator.

## Getting the Firmware File

Attempt the easiest way first, if the supplier has a website which provides firmware updates, you can download the firmware file as a whole.

If the firmware update can be directly downloaded only  by the device, sniff the communication with wireshark and get the firmware file that way.

If none of the steps are available, download the eeprom image through the JTAG connector using Bus Pirate and OpenOCD.

To get the information from the firmware file do the following:
```

$ file DVA-5592_A1_WI_20180405.sig

DVA-5592_A1_WI_20180405.sig: data

$ binwalk DVA-5592_A1_WI_20180405.sig

DECIMAL HEXADECIMAL DESCRIPTION
```

---------------------------------------------------
```

512 0x200 JFFS2 filesystem, little endian

24379992 0x1740258 gzip compressed data, from

Unix, last modified:

2018-04-11 10:40:16
```

Extract the content from the firmware itself by installing Jefferson to extract files from the JFFS2 file

system.

You can use binwalk to extract content from the firmware by doing the following:
```

$ binwalk -e DVA-5592_A1_WI_20180405.sig

$ ls -lh _DVA-5592_A1_WI_20180405.sig.extracted

-rw-rw-r-- 1 val val 30K ott 21 13:28 1740258

-rw-rw-r-- 1 val val 24M ott 21 13:27 200.jffs2

drwxrwxr-x 5 val val 4,0K ott 21 13:28 jffs2-root

$ file 1740258

1740258: POSIX tar archive (GNU)

$ tar -tvf 1740258

drwxr-xr-x l.fornalczyk/adb boards/

drwxr-xr-x l.fornalczyk/adb boards/963138_VD5….ipk
```

To look at the extracted files:
```

$ ls jffs2-root/

fs_1 fs_2 fs_3
```

There are a total of three file systems here, “/boot” and “/” into two parts:
```
$ ls -lh fs_1

-rw-r--r-- 1 val val 0 ott 21 13:28 a

-rw-r--r-- 1 val val 260K ott 21 13:28 cferam.000

-rw-r--r-- 1 val val 1,2M ott 21 13:28 vmlinux.lz
```
cferam.000 is the boot loader image which is based on the Broadcom Common Frimware Enviroment while vmlinux.lz is the kernel and is a CFE compressed format.

When it comes to the other files /sbin/init is missing, but busybox is there.
```
$ ls -lh fs_2/bin/busybox -rwsr-sr-x 1 val val 382K fs_2/bin/busybox

$ strings fs_2/bin/busybox …

BusyBox v1.17.3 (2018-04-11 12:29:54 CEST) …

$ arm-linux-readelf -a fs_2/bin/busybox …

… program interpreter: /lib/ld-uClibc.so.0]

$ ls -lh fs_2/lib/ld-uClibc* -rwxr-xr-x ld-uClibc-0.9.33.2.so

lrwxrwxrwx ld-uClibc.so.0 -> ld-uClibc-0.9.33.2.so

$ ls -l fs_3/lib/libgcrypt.so.11*

lrwxrwxrwx libgcrypt.so.11 -> libgcrypt.so.11.5.3 -rwxr-xr-x libgcrypt.so.11.5.3

The Boot output on the serial console went something like this:
```
...
```
CFE version 1.0.38-118.3-S for BCM963138 (32bit,SP,LE)

generic
```
...
```
Chip ID: BCM63136B0, ARM Cortex A9 Dual Core: 1000MHz

Total Memory: 268435456 bytes (256MB)

NAND ECC BCH-4, page size 0x800 bytes, spare size 64 bytes

NAND flash device: , id 0xc2da block 128KB size 262144KB
```
...
```
Linux version 3.4.11-rt19 (l.fornalczyk@quelo) (gcc version

4.5.4 20120306 (prerelease) (Linaro GCC 4.5-2012.03) )
```
...
```
CPU: ARMv7 Processor [414fc091] revision 1 (ARMv7)
```
...
```
jffs2: version 2.2 (NAND) (SUMMARY) (ZLIB) (LZMA) (RTIME)
```
...

...
```
[2.502000] Found YAPS PartitionSplit Marker at 0x080FFF00

[2.503000] Creating 8 MTD partitions on "brcmnand.0":

[2.504000] 0x000000000000-0x000000020000 : "CFE”

[2.506000] 0x000007f00000-0x000008100000 : "bootfs_1”

[2.508000] 0x000008100000-0x00000fbc0000 : "rootfs_1”

[2.510000] 0x000000020000-0x000007ce0000 : "upgrade”

[2.512000] 0x00000fbc0000-0x00000fdc0000 : "conf_fs”

[2.513000] 0x00000fdc0000-0x00000fe00000 : "conf_factory”

[2.515000] 0x00000fe00000-0x000010000000 : "bbt”

[2.517000] 0x000000000000-0x000010000000 : "flash” ...

Init started: BusyBox v1.17.3 (2018-04-11 12:29:54 CEST)

starting pid 235, tty '': '/etc/init.d/rcS S boot’

Starting boot.sh ... Restore passwd .... Restore group ....

Starting /etc/rc.d/S11services.sh ...

Starting Configuration Manager (B)
```
…
```
CM TR-181 ready CM TR-98 ready Epicentro Software Version: DVA-5592_A1_WI_20180405 Epicentro Platform Version: 6.0.0.0028 ... Starting /etc/rc.d/S13acsd.sh ... Starting /etc/rc.d/S20voip.sh ... Starting /etc/rc.d/S60ipsec.sh ... Starting /etc/rc.d/S70vpn.sh ... Starting /etc/rc.d/S94printkd.sh ...
```
Searching Epicentro Software on the internet gives the Original Design Manufacturer ADB adbglobal.com.

<![if !supportLists]>· <![endif]>Through this, we found out that the processor is an ARMv7 Cortex-A9 Multicore

<![if !supportLists]>· <![endif]>That there is 256Mb NAND Flash

<![if !supportLists]>· <![endif]>The Linux Version is 3.4.11-rt19

<![if !supportLists]>· <![endif]>uClibic version is 0.9.33.2

<![if !supportLists]>· <![endif]>BusyBox version is 1.17.3

<![if !supportLists]>· <![endif]>Libgcrypt version is 1.4.5

<![if !supportLists]>· <![endif]>Epicentro software is by ADB or adbglobal.com

## References

- Digiampietro(https://www.digiampietro.com/myfiles/dva/iot-rev-engineering.pdf){:target="_blank"}