---
title: "Protocol Detector"
date: "2017-09-09"
image: assets/images/networking-100735059-large.jpg
author: jpalanco
layout: post
tags: [ network, protocol, tools, yara ]
categories: [ Projects ]
---

ProtocolDetector is am open source python library I developed for [Dinoflux](https://www.dinoflux.com). This library aims to provide an easy-to-use mechanism to integrate protocol detection capabilities into your python applications.

- Uses yara as engine for parsing packets
- Supports network live capture
- Supports pcap reading
- Supports socks proxy to filter local address
- It comes with CLI for working out of the box
- JSON output for easy parsing

## Install

 

sudo pip install git+git://github.com/jpalanco/ProtocolDetector.git

## Command Line

Analyze a pcap file:
```
ProtocolDetector -p example.pcap
```
 

Analyze iface (real-time):
```
ProtocolDetector -i eth0
```
 

Example output:

```json
{'dport': 1604, 'src': '192.168.1.10', 'dst': '94.73.33.36', 'sport': 49181, 'protocols': [darkcomet]}
```
 

## API

``` python
from ProtocolDetector.Engine import get\_rules, perform\_check
import dpkt

pcap_path='dump.pcap'
pcap_file = open(pcap_path)
pcap=dpkt.pcap.Reader(pcap_file)

options = { 'mode': 'default',
            'socks_proxy': False,
            'remove_local' : False,
            'pcap_path': pcap_path,
            'iface': None,
            'rules' : get_rules() }

for ts, buf in pcap:
        results = perform_check(buf, options )
        print results
```
 

## Adding Protocols

Adding protocols is pretty easy, we only need to create a yara rule and place it at ProtocolDetector/rules/ directory and add it to the index.yar file. Let's see a few examples of protocol rules:

``` 
rule ssl : protocols
{
  meta:
    author = "Jose Ramon Palanco <jpalanco@gmail.com>"
    description = "SSL"
  strings:
    $content_type = /(\x13|\x14|\x15|\x16|\x17)/
    $version_tsl_1_2 = { 03 03 }
    $version_tsl_1_0 = { 03 01 }
    $version_tsl_3_0 = { 03 00 }

  condition:
    $content_type at 0 and ($version_tsl_1_2 at 1 or $version_tsl_1_0 at 1 or $version_tsl_3_0 at 1)
}
```

In this example, we can see that at position 0 (the first byte of the payload) we will need to find the content-type, and it should be 13h, 14h, 15h, 16h or 17h. If we found that we will require to find a valid version. In this example, I cover TSL 1.0, TSL 1.2 and TSL 3.0.

```
rule njrat : protocols
{
  meta:
    author = "Jose Ramon Palanco <jpalanco@gmail.com>"
    description = "njRAT Protocol"
  strings:
    $header = /\d{1,6}\x00/
    $sep = { 7C 27 7C 27 7C }
  condition:
    $header at 0 and $sep
}
```

This example detects njRAT, a common Remote Administration Tool. In this case, we need to find at position 0, from 1 to 6 integers followed by a null byte and the separator which is 0x7C277C277C.

 

You can find more protocols implemented at my github repository [https://github.com/jpalanco/ProtocolDetector](https://github.com/jpalanco/ProtocolDetector)

Happy hacking!!
