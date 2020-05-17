---
title: "STM32 debugging with ST-Link"
date: "2019-01-30"
image: assets/images/STM32.jpeg"
author: jpalanco
layout: post
tags: [ ST-Link, STM32]
categories: [ hw-hacking, iot-security]
---

In this article I wil explain how can we program, debug and dump a firmware from STM32 boards. For this, we will need a [st-link v2 programmer](https://www.amazon.es/gp/product/B07HGLVTHQ/ref=as_li_tl?ie=UTF8&camp=3638&creative=24630&creativeASIN=B07HGLVTHQ&linkCode=as2&tag=jpalanco-21&linkId=da679f0633b697ec3001fc016aba0de8). The first step is to download the datasheet related to out chipset and locate the pinout to connect out st-link v2 programmer:

- Connect the CLK pad on the pcb to SWCLK on the st-link.
- Connect DAT pad to SWDIO.
- Connect grounds GND and ST-link GND together.

I will explain how to do it using a Mac, but using other operating systems it may be similar. We will need to install stlink software, in mac with brew we can do it like this:
```
$ brew install stlink
```
For connecting the stlinkwe will execute:
```
$ stlink 
```
In general it will open localhost:4242, we have to note this address for later

Optionally you can use openocd, in this case it will listen at localhost:4444 by default:
```
$ openocd -f /usr/local/Cellar/open-ocd/0.10.0/share/openocd/scripts/interface/stlink-v2.cfg -f /usr/local/Cellar/open-ocd/0.10.0/share/openocd/scripts/target/stm32f1x.cfg
```
We will need also gcc arm for cross-compiling:
```
$ brew tap osx-cross/arm

$ brew install arm-gcc-bin
```
Remember add symbols using -g build option in gcc. For uploading our we will load our elf in gdb:
```
$ arm-none-eabi-gdb -tui /path/to/file.elf
(gdb) target remote localhost:4242
(gdb) load
(gdb) break main
```
We can connect to openccd using radare2:
```
$ r2 -a arm -b 32 -D gdb gdb://127.0.0.1:4444
```
For dumping the memory we can do:
```
$ st-flash  read /tmp/output.bin 0x8000000 0x8000
```
**WARNING**: When working, and powering the STM target board from the programmer, if you plug in the USB port at the same time, remove the power (orange) wire first, and power the board from USB otherwise you may burn your board.
