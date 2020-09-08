---
title: "Firmware Reversing: FACT Core"
date: "2020-8-9"
image: assets/images/factcore.png
author: name
layout: post
tags: [ DECT, Snifing, deDECTed]
categories: [ sniffing ]
---

Firmware analysis can be a tough challenge with a lot of tasks involved in its effective execution.

Many of these tasks can be done automatically through new approaches or through the implementation of existing tools.

Through this, a security analyst has the capability to focus on the task of analyzing the firmware and finding its vulnerabilities.

FACT implements this automation leading to an overall more complete analysis as well as allowing for an enormous boost in speed in venerability hunting.

## Firmware Extraction

The extraction process of a firmware image could lead to a lot of time consumption.

This is due to the fact that, at first, you need to identify the container format, and afterwards, you need to find the appropriate unpacker for the job at hand.

If no extraction tool is available, you might even have to try a file carver like binwalk to extract at least a few of the firmware components.

When this task is executed effectively, you have to redo these tasks for each layer multiple times.

FACT can automate the entire process.

## Firmware Analysis

The next thing you want to do is find out as much as you can about the firmware in order to identify the potential risks and vulnerabilities.

FACT can solve these challenges, including:  
Software Identification, such as the OS used, programs present, versions of the programs, the services which are started on boot, and any well-known vulnerabilities.

It can find login credentials as well as hard-coded passwords with crypto material detection such as private keys and certificates.

By far one of the best features is the detection of CPU architecture which is needed for emulation and disassembling and you can even check if an executable is utilizing QEMU and look for implementation flaws or CWEs.

## Firmware Comparison

You might also need to compare firmware samples if you need to know where a manufacturer fixed an issue in a new firmware version.

You might also be interested in knowing if the firmware on your device is the original one provided by the manufacturer itself.

If these differ, you want to figure out which parts are changed for further investigations.

FACT automates these challenges by identifying the changer or equal files as well as changed software versions.

## Finding Other Affected Firmware Images

When you find a new vulnerability or a new container format, you might need to know if other firmware images share your findings.

FACT stores all firmware files and analysis results in a searchable database, allowing you to search byte patterns on all unpacked files as well as any kind of result.

## How to Install

The Firmware Analysis and Comparison Tool, also known as Fraunhofer’s Firmware Analysis Framework or FAF can automate most of the firmware analysis process by unpacking arbitrary firmware files and processes several analyses.

It can compare several images or single files.

Unpacking, analysis and comparisons are based on plug-ins which guarantee maximal flexibility and expandability.

FACT is designed as a multiprocess application, and as such, the more cores and ram you have, the better it can perform.

When it comes to the requirements, on the hardware side of things, you need a minimum of 4 cores and 8 GB of ram with 10 GB of disk space for it to work, however, the recommended amount is 16 cores and 64 GB of ram with over 10 GB of space for it to work effectively.  
When it comes to the requirements, on the software side of things, you need git, python 3.5 or 3.8, and a Linux operating system.

The 10 GB are required to set up the FACT code, container and binaries.

Additional space is required for result storage, but these can be done on separate partitions or drives.

You can theoretically install FACT on any Linux distribution out there, but the installer itself natively works on Ubuntu 16.04, 18.04 and 20.04, as well as Ubuntu 19.04, Debian 9 or 10, and Kali 201.3 and 2019.4.

The installation is wrapped in a single script.

To start using FACT, you can execute the start_all_installed_fact_components scripts.

These scripts detect all installed components automatically.

These can be initiated by typing the following command:
```

$ ./start_all_installed_fact_components
```

After this, FACT can be accessed on [http://localhost:5000](http://localhost:5000) and [https://localhost](https://localhost) (nginx).
```
You can shutdown the system by pressing CTRL+C or by sending a SIGTERM to the start_all_installed_faf_components script.
```
## How to Extend

FACT can be extended through plug-ins.

The REST_API is available to connect to external tools.

Almost all features of the web-interface are available through REST as well.

Here is how FACT initial analysis works

[link] (https://raw.githubusercontent.com/wiki/fkie-cad/FACT_core/images/fact_concept_initial_analysis.png)
Here is how FACT compare works

[link] (https://raw.githubusercontent.com/wiki/fkie-cad/FACT_core/images/fact_concept_compare.png)

There are a total of three types of plug ins, including an unpacker, analysis, and compare.

FACT is based on a plug-in concept.

Extractors, analysis features and compare functionalities are implemented as plug-ins.

## The REST API

The FACT REST API is intended to offer close to 100% functionality of FACT in a script-able and integrate-able interface.

The API does no comply with all REST guidelines perfectly but it allows understandable and efficient interfacing.

All of the data is sent as a message body and all of the data is received from the API is of application/json format.

This allows easy integration into most programming languages, most commonly javascript and python.

Since json does not support binary data, all binary data is additionally encoded in base64.

The API does offer a number of URL parameters to go with GET requests.

These parameters for each endpoint are listed through tables at the beginning of the endpoint.

The API is not versioned and is subject to change.

When it comes to authentication, if the authentication option is enabled in the configuration, each REST request has to be accompanied by an API key in the HTTP header.

If your user has been given the exemplary key ABCDEFG= , a request to the /rest/binary endpoint should look something like this:
```
curl http://localhost:5000/rest/binary/ceb0b13da1e765ec105460cf68367b78ed78b99fcbdd7654999a07b5b87e8f16_31 -X GET --header 'Authorization: ABCDEFG=' -L.
```

## References

- fkie-cad (https://fkie-cad.github.io/FACT_core/){:target="_blank"}