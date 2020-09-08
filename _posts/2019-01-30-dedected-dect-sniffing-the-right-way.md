---
title: "deDECTed – DECT Sniffing the Right Way"
date: "2020-8-9"
image: assets/images/dectsniffing.jpg
author: name
layout: post
tags: [ DECT, Snifing, deDECTed]
categories: [ sniffing ]
---

Before we begin this guide there is something important that needs to be discussed.

Recording phone conversations without having consent from the user is highly illegal within the United States as well as in many other countries.

This guide is intended to teach you how to do the task on your own equipment for the purposes of testing.

Remember to record your own DECT’s, not your acquaintances.

The hardware used in this guide includes a Backtrack 5 Final x86 KDE with Kernel 2.6.38 installation of Linux, an Original Dosh and Amand Type II PCMCIA Card, and a set of SIEMENS C1 DECT phones set up in repeater mode.

With that out of the way, let us begin this adventure.

## What exactly is DECT?

The term “DECT” can be confusing to a lot of people as not everyone can get it initially.

The word DECT stands for Digital Enhanced Cordless Telecommunications and is a wireless standard that is often used for landline phones.

Wireless communication has been given a massive boost thanks to the introduction of the wireless standard.

DECT can be described as a technology that is to telephony what WiFi is to the internet.

DECT has several advantages, such as a long-range of up to 40 meters indoors or 300 meters outdoors, it is very energy-efficient, can connect through a separate frequency range that is not dependent on WiFi and offers better quality of sound than with any of the previous standards.

A DECT system always contains two components that constantly communicate with each other which are the base station and the handset.

The base station is the bridge between the telephone and the internet connection.

This can be in the form of a simple DECT station or without an answering machine or a DSL router with DECT Function.

The base station continuously sends a “beacon signal” which can be received by a handset in the vicinity.  
This signal provides the handset with the necessary information to allow it to connect and send data through the base station.

They are both synchronized and can make a phone call through a cordless solution.

It originated in Europe and it is the universal standard which replaced earlier cordless phone standards such as 900 MHz CT1 and CT2.

## Installing Dedected

When you want to install Dedected on Backtrack 5, you have two options:  
Use Dedected from the Backtrack Repository or Compiling it on your own if you feel like experimenting.

In order to install it from the source, open the terminal and type the following commands:

```

root@bt:~# prepare-kernel-sources

root@bt:~# cd /usr/src/linux

root@bt:~# cp -rf include/generated/* include/linux/

root@bt:~# cd /pentest/telephony

root@bt:~# svn co https://dedected.org/svn/trunk dedected_svn

root@bt:~# cd dedected_svn/com-on-air_cs-linux/

root@bt:~# make && make -C tools

Install from repository

root@bt:~# apt-get update

root@bt:~# apt-get install dedected
```

It is recommended that you have the tool Audacity if you are serious about recording phone conversations, so make sure to install that as-well.

Load the Drivers
```

root@bt:~# cd /pentest/telephony/dedected/com-on-air_cs-linux

root@bt:~# make node

root@bt:~# make load
```

## Start Scanning for Fixed Parts or Fp, the DECT Base Stations

To do this, enter the following commands in the terminal:
```

root@bt:~# cd /pentest/telephony/dedected/com-on-air_cs-linux/tools

root@bt:~# ./dect_cli
```

If you have a hard time, make sure to type “help” to get the full usage type.

If you are a resident of the United States, ensure that you switch to the US or DECT 6 band through the “band” command.

Next, Enable verbosity:  
**verb**

Start scanning fpscan.

After scanning multiple times, disable verbosity and stop the scanning process.

**verb stop**

## How to Ignore Other Phones

To ignore other phones, you need to start a callscan.

To do this, type **callscan**.

In the next step, you need to get your DECT handset and make a test call.

Wait until you see the phonecall.

It is also sufficient if you just get the dialing tone initially.

You should be seeing something like this in the terminal:

### found new call on 00 92 41 32 72 on channel 7 RSSI 42

**stop**

Now dump all found calls

**dump**

Now comes the important bit, make sure to ignore every other phone except yours through the following command:

ignore 01 30 95 13 37

## How to Record the Call

This is important, make sure to never record anyone without permission or consent, as you can get in serious trouble with the law.

That being said, in order to start recording every phone call automatically that Dedected can detect, use the following command:  
**autorec**

It should look something like this:

### starting autorec

### stopping DIP

### starting callscan

### trying to sync on 00 82 ab b0 29

### got sync

### dumping to dump_2011-06-11_21_37_37_RFPI_00_82_ab_b0_29.pcap

### stopping DIP

After you hang up the dumping should stop.

## Decoding the Call Stream

To decode the call stream, you first need to stop the autorec.

Do this by typing **stop.**

Now, to decode the audio stream into a raw packet dump, type the following command:

root@bt:~# ./decode.sh

You should be done.

## Importing the Streams into Audacity

In order to listen to the recorded calls, you need to use an application.

The most recommended one to use in this case is Audacity.

You need to start Audacity first through alt+f2 and type audacity.

Press enter, and once the application opens, you can import the fixed-part and the portable-part.wav files from /pentest/telephony/dedected/com-on-air_cs-linux/tools through File -> import -> audio or simply through ctrl+shift+I.

Import the files which end in .pcap_fp.ima.g721.wav and .pcap_pp.ima.g721.wav.

Play the recording through the play button.

## Cleaning Things Up

Reload the drivers by typing the following command:
```

root@bt:~# cd /pentest/telephony/dedected/com-on-air_cs-linux

root@bt:~# make reload
```

If you want to clean up, type the following command:

```
root@bt:~# cd /pentest/telephony/dedected/com-on-air_cs-linux

root@bt:~# make unload

root@bt:~# rm /dev/coa
```
And you are finally done.

Congratulations, you have successfully learned how to record DECT calls with Dedected.  
Keep in mind that this guide was made with testing purposes in mind, and you should in no way, shape or form record someone who has not given you consent in doing so.

#References 

- instructables https://www.instructables.com/id/Telephony-DECT-Sniffing-with-Dedected/){:target="_blank"}