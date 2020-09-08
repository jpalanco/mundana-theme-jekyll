---
title: "Inside HAVEX"
date: "2014-07-24"
image: assets/images/HAVEX/havex.jpg
author: jpalanco
layout: post
tags: [ havex, malware, SCADA, ICS, OT, OPC, reversing ]
categories: [ reversing ]
---

We have analyzed a sample of Havex and from there, we have prepared a report of behavior. Throughout the report you will find all the details of operation we have located from our analysis.

> Special thanks to **Manu Quintans** and **Andriy Brukhovetskyy**. They helped us during certain phases of the analysis.

----------


----------

# 1.- Changelog

| Version date     | Author                       | Modification        |
 ----------------- | ---------------------------- | ------------------
| 15/07/2014 | Jose Palanco                  |Document creation|
| 15/07/2014 | Guillermo Campillo            | Installer Analysis|
| 18/07/2014 | Carlos Antonini| Static Analysis  |
| 22/07/2014 | Jose Palanco | Static & Dynamic Analysis|
| 23/07/2014 | Guillermo Campillo | Static & Dynamic Analysis|
| 23/07/2014 | Jose Palanco | Final Review |

# 2.- General Information


The installation procedure is carried out by installing a modified version of the *mbcheck* software 

- http://www.mbconnectline.com/index.php/en/

The original was replaced by the backdoored version and was a server for customers.

From mbconnectline site:

The MB Connect Line GmbH offers universal solutions for worldwide remote maintenance of machinery and equipment. Werner Belle and Siegfried Müller founded the company in 1997. The Headquarters, including sales, is located in Ilsfeld.  Technical development and production occur in Dinkelsbuehl.

The specialists at MB Connect Line have years of experience and extensive know-how. Customized solutions for customer-specific tasks are a strength of MB Connect Line. For example, the implementation of proprietary protocols, and integration of special hardware (i.e.Cisco ASA) are some of the tasks we have solved in the past. Packaging machines, production lines, solar power plants, or Biogas plants – MB Connect Line has developed remote maintenance solutions to fit many application areas.

# 3.- General Information

The following report analyzes the behavior of a sample of Havex, specifically the 043 version. The mbcheck installer, uncompress a dll file, save it at `%TEMP%\mbcheck.dll` and execute it silently.

To summarize, the sample performs the following actions: 

1. Is self-installed persistently in the system
2. Scans computers on the same network
3. Detects if any of the computers have installed a OPC server
4. Scans the OPC services available and gets their names tags
5. Encrypts the information obtained
6. Sends the information to the control servers

# 4.-  Statistic analysis

## 4.1 File Info


**Name**                
`mbCHECK.dll`

**Original  name**       
`7CFC9E59D3A.dll`

**Imports**            

- kernel32.dll
- user32.dll
- advapi32.dll
- shell32.dll
- ole32.dll
- wininet.dll
- crypt32.dll

**imphash**             
`a85560a14f8135bb751c39cfa37081ae`

**MD5**                 
`51502d7d6d188ad87213ca5942f232cf`

**SHA1**                
`317fd58d53aa3fe0fec209702a879aefb77c148c`

**SHA256**          
`d5687b5c5cec11c851e84a1d40af3ef52607575487a70224f63458c24481076c`

**ssdeep**              
`12288:x+Y5rLl9CywddByZqwgaatNgdaLEhjKdT: AY5rLl9Cyw/ByEwTatNgdYEhjKdT`

**File size**           
`427.0 KB ( 437248 bytes )`

**File type**           
`Win32 DLL`

**Magic literal**       
`PE32 executable for MS Windows (DLL) (console) Intel 80386 32-bit`

**TrID**                
`InstallShield setup (48.1%)`

- Win32 Executable MS Visual C++ (generic) (34.9%)
- Win32 Dynamic Link Library (generic) (7.3%)
- Win32 Executable (generic) (5.0%)
- Generic Win/DOS Executable (2.2%)

**Target machine**           
Intel 386 or later processors and compatible processors

**Compilation timestamp**    
2014-04-11 05:37:36

**Link date**                
6:37 AM 4/11/2014

**Entry Point**              
0x00024A7D

## 4.2 PE Sections

| Name | Virtual Address | Virtual Size | Raw Size     | Entropy |MD5                      
 ----------------- | ---------------------------- | ------------------
| .text  | 4096|323011|323072|6.70               |ced183458a2afdd2b540df062885dfc4|
| .rdata  | 323011|   62607   |62976 |4.76     | 9a30e2cc0b8b39737b645163349100a7|
| .data | 393216|31356 | 23040 |5.13|19e085a7a23b4f281b2879d13a0ee5bf|
| .rsrc | 425984|1208 |1536| 6.77|25d94bb318bf564a26b8e3db16d0ec4b|
| .reloc | 430080|25274 |25600| 5.24 |9b44df053516303f2012e1c9768af11a|


## 4.3 Resoures

- **Name**       `MANIFEST`
- **File name**  `MANIFEST`
- **File type**  `Text`
- **Md5**        `24D3B502E1846356B0263F945DDD5529`
 
- **Name**       `ICT`
- **File name**  `ICT.bz2`
- **File type**  `bzip2 compressed data, block size = 900k`
- **Md5**        `e99d7d4bfc9eeb316ac7a5e4a29b7035`


## 4.3.1 ICT – uncompressed

When uncompressing the resource, we get an encrypted file. The details to decipher it are available in **Annex “Sample Configuration”.**

- **Name** `ICT.dump`
- **File type** `data`
- **Md5**  `e7e25cceb1a85945f484ab0d2ff61bf8`

## 4.4 Exports

The library exports only one function: `RunDLLEntry`

## 4.5 VirusTotal

**Detection ratio: 31/53**

| AV Company | Malware Signature |                     
 ----------------- | ---------------------------- | ------------------
| 
AVG | Generic36.PAN
Ad-Aware|   Trojan.Generic.11277511
AntiVir |TR/Bublik.clgx.1
Antiy-AVL   |Trojan/Win32.Bublik
Baidu-International|    Trojan.Win32.Bublik.apZR
BitDefender |Trojan.Generic.11277511
Comodo| UnclassifiedMalware
DrWeb   |Trojan.Inject1.42303
ESET-NOD32  |Win32/Gertref.E
Emsisoft    |Trojan.Generic.11277511
F-Secure    |Backdoor:W32/Havex.A
Fortinet    |W32/Bublik.CLGX!tr
GData   |Trojan.Generic.11277511
Ikarus  |Trojan.Bublik
K7AntiVirus |Riskware
K7GW    |Trojan
Kaspersky   |Trojan.Win32.Bublik.clgx
McAfee  |RDN/Generic.bfr!gf
McAfee-GW-Edition   |RDN/Generic.bfr!gf
MicroWorld-eScan    |Trojan.Generic.11277511
Microsoft|  Trojan:Win32/Malagent!gmb
Norman| Troj_Generic.UCKCK
Panda   |Trj/OCJ.E
Qihoo-360|  Win32/Trojan.880
Sophos| Mal/Generic-S
Symantec    |WS.Reputation.1
TrendMicro| TROJ_GEN.R0CBC0DEF14
TrendMicro-HouseCall    |TROJ_GEN.R0CBC0DEF14
VBA32|  Trojan.Bublik
VIPRE   |Trojan.Win32.Generic!BT
nProtect    |Trojan.Generic.11277511

## 4.6 Functions
Function svcprocess043.dll!W_CreateFileqln_dbx

This function is responsible for writing the qln.dbx file in the %TEMP% directory; it is also responsible for sending the full path.

![]({{ site.baseurl }}/assets/images/HAVEX/002.png)

Function svcprocess043.dll!W_ConnectoCnC

![]({{ site.baseurl }}/assets/images/HAVEX/003.png)

This function is divided into three parts:

> 1. Prepares the raw data and checks the internet connection.
> 2. Obtains parameters.
> 3. Saves and closes the connections.

 1. Checks and prepares the connection for the API: InternetConnectW

![]({{ site.baseurl }}/assets/images/HAVEX/004.png)

 2. Prepares the parameters to send to the URL, later using the API HttpOpenRequest to send requests to the C&C

![]({{ site.baseurl }}/assets/images/HAVEX/005.png)

![]({{ site.baseurl }}/assets/images/HAVEX/006.png)

![]({{ site.baseurl }}/assets/images/HAVEX/007.png)

As we can see, this makes a request to a C&C and we capture the TCP stream with Wireshark

![]({{ site.baseurl }}/assets/images/HAVEX/008.png)

3. If the server sends a command to download any file, in this part, it gets the file from the server and stores it using the API InternetReadFile. Then it closes connections by using the API.

![]({{ site.baseurl }}/assets/images/HAVEX/009.png)

![]({{ site.baseurl }}/assets/images/HAVEX/010.png)

![]({{ site.baseurl }}/assets/images/HAVEX/011.png)

Complete graph

![]({{ site.baseurl }}/assets/images/HAVEX/012.png)

Function svcprocess043.dll!W_CreateFileXmd

Creates an encrypted file with xmb extension. The files are downloaded from C&C.

![]({{ site.baseurl }}/assets/images/HAVEX/013.png)

Complete graph:

![]({{ site.baseurl }}/assets/images/HAVEX/014.png)

Function svcprocess043.dll!W_CoInterface

Initializes the COM library using the calling thread, and makes a new thread. 
This function returns a CLSID to be used for communicating with the OPC protocol to the PLC devices.

| CLSID | Name |                     
 ----------------- | ---------------------------- | ------------------
9DD0B56C-AD9E-43EE-8305-487F3188BF7A    | IID_IOPCServerList2
13486D51-4821-11D2-A494-3CB306C10000|   CLSID_OPCServerList

![]({{ site.baseurl }}/assets/images/HAVEX/015.png)

Complete graph:

![]({{ site.baseurl }}/assets/images/HAVEX/016.png)

Function svcprocess043.dll!W_RegisterClassExW

This function creates a new class and assigns the method. The class name is “button,” and points to the  `svcprocess043.dll!` `W_CreateMainWind` address.

It creates a new class under the name "`21f34`" with the following structure:

![]({{ site.baseurl }}/assets/images/HAVEX/017.png)

    typedef struct tagWNDCLASSEX {
    UINT      cbSize;
    UINT      style;
    WNDPROC   lpfnWndProc;
    int       cbClsExtra;
    int       cbWndExtra;
    HINSTANCE hInstance;
    HICON     hIcon;
    HCURSOR   hCursor;
    HBRUSH    hbrBackground;
    LPCTSTR   lpszMenuName;
    LPCTSTR   lpszClassName;
    HICON     hIconSm;
    } WNDCLASSEX, *PWNDCLASSEX;

In this structure, the most important is the class name and the procedure to run.

The method of this class is:


![]({{ site.baseurl }}/assets/images/HAVEX/018.png)

![]({{ site.baseurl }}/assets/images/HAVEX/019.png)

![]({{ site.baseurl }}/assets/images/HAVEX/020.png)

![]({{ site.baseurl }}/assets/images/HAVEX/021.png)

![]({{ site.baseurl }}/assets/images/HAVEX/022.png)

![]({{ site.baseurl }}/assets/images/HAVEX/023.png)

![]({{ site.baseurl }}/assets/images/HAVEX/024.png)

After creating and registering the new class will launch a hidden window with this class.

![]({{ site.baseurl }}/assets/images/HAVEX/025.png)

![]({{ site.baseurl }}/assets/images/HAVEX/026.png)

![]({{ site.baseurl }}/assets/images/HAVEX/027.png)

![]({{ site.baseurl }}/assets/images/HAVEX/028.png)

Function svcprocess043.dll!W_injectDll

This function loads the previously downloaded dll and runs it. 

**Step 1**

Using the svcprocess043.dll!W_GetLibraryW function, it loads the downloaded dll through LoadLibraryW

![]({{ site.baseurl }}/assets/images/HAVEX/029.png)

![]({{ site.baseurl }}/assets/images/HAVEX/030.png)

**Step 2**

After loading the dll in memory, it calls to the rundll method

![]({{ site.baseurl }}/assets/images/HAVEX/031.png)

Complete graph:

![]({{ site.baseurl }}/assets/images/HAVEX/032.png)

# 5.- Dynamic Analysis

## 5.1 Enviroment

To run the sample, we need a PLC exporting via OPC the tag states. During the analysis we used the Matrikon OPC server.

![]({{ site.baseurl }}/assets/images/HAVEX/033.png)

And the browser to verify that the server was running fine.

![]({{ site.baseurl }}/assets/images/HAVEX/034.png)

## 5.2 Persistence

To start the execution, the sample exports the function RunDLLEntry. The sample installs itself in the system at `%SYSTEMROOT%\System32\svcprocess043.dll`

![]({{ site.baseurl }}/assets/images/HAVEX/035.png)

![]({{ site.baseurl }}/assets/images/HAVEX/036.png)

![]({{ site.baseurl }}/assets/images/HAVEX/037.png)

Starting from Windows 7, the sample is copied to `%ALLUSERSPROFILE%\svcprocess043.dll`

![]({{ site.baseurl }}/assets/images/HAVEX/038.png)

The malware uses the registry to be persistent.

![]({{ site.baseurl }}/assets/images/HAVEX/039.png)

Value:

![]({{ site.baseurl }}/assets/images/HAVEX/040.png)

During the execution of this piece of malware, it creates new threads, calling itself during the execution and injecting itself into defined processes, according to the configuration. This sample is injected into Explorer.exe. Later we will see how the sample configuration allows select the process in which will be injected.

![]({{ site.baseurl }}/assets/images/HAVEX/041.png)

The process modifies the registry by creating new keys.

![]({{ site.baseurl }}/assets/images/HAVEX/042.png)

## 5.3 Installation flowchart

![]({{ site.baseurl }}/assets/images/HAVEX/043.png)

## 5.4 Behavior

During execution, the sample creates several files `*.XMD,.* DAT, *.DLLs`, that are deleted after being used.

The generated DLLs also contain resources that can be deciphered using the technique of Annex “Configuration Extractor”.

The sample gets lot of system information, OPC services information, Remote Access credentials, then encrypts and sends the information to the reporting server.

## 5.5 Changes to filesystem

[a-fA-F0-9].tmp | empty                    
 ----------------- | ---------------------------- | ------------------
[a-fA-F0-9].dat |  scanner log
[a-fA-F0-9].tmp.xmd |   crypted file download from C&C
[a-fA-F0-9].tmp.yls  |    crypted report
[a-fA-F0-9].tmp.dll |  

Example:

    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\10.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\10.tmp.yls
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\7.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\7.tmp.xmd
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\8.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\8.tmp.dll
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\9.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\9.tmp.yls
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\A.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\A.tmp.xmd
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\B.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\B.tmp.dll
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\C.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\C.tmp.xmd
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\D.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\D.tmp.dll
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\E.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\E.tmp.dat
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\F.tmp
    
    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\F.tmp.yls

    C:\\Documents and Settings\\sandbox\\Configuración local\\Temp\\qln.dbx

-----------------------------------------------------------------------

### 5.5.1 File *.dat:

The DAT file contains a log on the analysis of OPC services.

DAT file before being deleted:

    Program was started at 23:43:45

    **************************************************************************

    23:43:56.0593: Start finging of LAN hosts…

    23:44:11.0906: Was found 1 hosts in LAN:

       01) [\\FALETE]

    **************************************************************************

    23:44:22.0046: Start finging of OPC Servers…

    23:46:13.0375: Was found 1 OPC Servers.

       1) [\\FALETE\Matrikon.OPC.Universal.1]

       CLSID:            {D7CA0556-C317-4512-8B8C-7543DD7F1626}

       UserType:         MatrikonOPC Universal Connectivity Server

       VerIndProgID:     Matrikon.OPC.Universal

       OPC version support: +++

    **************************************************************************

    23:46:20.0484: Start finging of OPC Tags…

    23:46:20.0546: Thread 01 running…

    23:46:22.0140: Thread 01 finished.

       1)[\\FALETE\Matrikon Inc +1-780-945-4011 http://www.matrikonopc.com]

       Saved in ‘OPCServer01.txt’

### 5.5.2 Files *.dll:

Dll| info                    
 ----------------- | ---------------------------- 
225.tmp.dll |     PE32 executable (DLL) (GUI) Intel 80386, for MS Windows
225.tmp.dll| MD5 7cff1403546eba915f1d7c023f12a0df
Resource |e5bad153e3c3ee1b735f1926ba573


Dll| info                    
 ----------------- | ---------------------------- 
228.tmp.dll |     PE32 executable (DLL) (GUI) Intel 80386, for MS Windows
228.tmp.dll MD5  | 840417d79736471c2f331550be993d79
Resource|         900adffc5180c10d463530e3753a3

             

Dll| info                    
 ----------------- | ---------------------------- 
228.tmp.dll |     PE32 executable (DLL) (GUI) Intel 80386, for MS Windows
22A.tmp.dll   | PE32 executable (DLL) (GUI) Intel 80386, for MS Windows
22A.tmp.dll MD5   | ba8da708b8784afd36c44bb5f1f436bc
Resource         |f84dd5aca779592badc5f55ac6c63



**NOTE**: This file is downloaded from the server.

This dll exports a function under the name “rundll” which initiates a scan of OPC services on the computer by using threads. This scan generates a log file, where all the information concerning the OPC services is stored. This is performed through the API call WNetEnumResourceW. The files are stored in the temp folder with .dat extension.
  

![]({{ site.baseurl }}/assets/images/HAVEX/044.png)

As seen in the picture, when the scanning process is started, the function opens the file in write mode to add the results. Each of the hosts found by WNetEnumResourceW function is then scanned to locate the OPC servers.

![]({{ site.baseurl }}/assets/images/HAVEX/045.png)

![]({{ site.baseurl }}/assets/images/HAVEX/046.png)

![]({{ site.baseurl }}/assets/images/HAVEX/047.png)

![]({{ site.baseurl }}/assets/images/HAVEX/048.png)

The result is a dat file with a report of the scanning process; this file is in plain text and can be read easily.

    Program was started at 13:04:57

    **************************************************************************

    13:08:11.0468: Start finging of LAN hosts…

    13:11:52.0156: Was found 1 hosts in LAN:

       01) [\\FALETE]

    **************************************************************************

    13:12:01.0484: Start finging of OPC Servers…

    13:12:29.0796: Was found 1 OPC Servers.

       1) [\\FALETE\Matrikon.OPC.Universal.1]

       CLSID:            {D7CA0556-C317-4512-8B8C-7543DD7F1626}

       UserType:         MatrikonOPC Universal Connectivity Server

       VerIndProgID:     Matrikon.OPC.Universal

       OPC version support: +++

    **************************************************************************

    13:16:19.0546: Start finging of OPC Tags…

    13:16:51.0734: Thread 01 running…

    13:16:59.0109: Thread 01 finished.

    13:17:07.0531: Thread 01 return error code: 0x00000103

       1)[\\FALETE\Matrikon Inc +1-780-945-4011 http://www.matrikonopc.com]

       Saved in ‘OPCServer01.txt’
After completing the scan, it reads the file and stores it in memory before deleting it, then it encrypts the content and saves it as a file with `yls` extension.

This dll does not seem to upload the file you just generated.

![]({{ site.baseurl }}/assets/images/HAVEX/049.png)

![]({{ site.baseurl }}/assets/images/HAVEX/050.png)

**228.dll analysis**

This dll shows a full system report in xml format (Annex), then saves encrypted yls extension.

The first thing done is creating the xml header:

![]({{ site.baseurl }}/assets/images/HAVEX/051.png)

The sample adds a node “receipt” which is the root node where all information is stored:

It checks whether the user is an administrator - in that case write adm. Walking several functions to get the information of the machine, both the processes and data are the same as the hardware and internet connections.

![]({{ site.baseurl }}/assets/images/HAVEX/052.png)

![]({{ site.baseurl }}/assets/images/HAVEX/053.png)

![]({{ site.baseurl }}/assets/images/HAVEX/054.png)

Finally, it creates a file with yls extension containing the xml encrypted data

![]({{ site.baseurl }}/assets/images/HAVEX/055.png)

### 5.5.3 File *.xmd:

This file is XORed with 1312312, compressed with bzip2 and base64 encoded. At `Annex “Scripts”`, you can find the script used to decrypt it.

Process for extracting the XMD:

    $ file 227.tmp.xmd

    227.tmp.xmd: ASCII text, with very long lines, with no line terminators

    $ base64 -d 227.tmp.xmd > 227.tmp.bz2

    $file 227.tmp.bz2

    227.tmp.bz2: bzip2 compressed data, block size = 900k

    $ bzip2 -d 227.tmp.bz2

    bzip2: Can’t guess original name for 227.tmp.bz2 -- using 227.tmp.bz2.out

    $ python decodeResource.py 227.tmp.bz2.out

    Good Job Mama!

    $ strings -e l 227.tmp.bz2.out.decode

    jjjjj

    $ file 227.tmp.bz2.out.decode

    227.tmp.bz2.out.decode: x86 executable (TV) not stripped

## 5.6 Changes to registry


![]({{ site.baseurl }}/assets/images/HAVEX/056.png)

![]({{ site.baseurl }}/assets/images/HAVEX/057.png)

Created:

| Key | Value |
|-----|-------|
| HKEY_LOCAL_MACHINE\\software\\microsoft\\Internet Explorer\\InternetRegistry fertger|49321511259132175120161FD80-c8a7af419640516616c342b13efab”|
| HKEY_LOCAL_MACHINE\\software\\microsoft\\Windows\\CurrentVersion\\Explorer\\BitBucket NukeOnDelete|  00000001|
| HKEY_LOCAL_MACHINE\\software\\microsoft\\Windows\\CurrentVersion\\Run svcprocess rundll32|"C:\\WINDOWS\\system32\\svcprocess043.dll", RunDllEntry Update |
| HKEY_CURRENT_USER\\software\\Microsoft\\Windows\\CurrentVersion\\Internet Settings\\Connections SavedLegacySetting |3C00000022000000010000000000000000000000000000000400000000000000105CAB43C5A4CF0101000000C0A8018E0000000000000000|
| HKEY_CURRENT_USER\\software\\Microsoft\\Windows\\CurrentVersion\\Run svcprocess rundll32 |"C:\\WINDOWS\\system32\\svcprocess043.dll"|
| HKEY_CURRENT_USER\\software\\SandboxAutoExec (Default)| 31|


## 5.7 Network services

The sample verifies that there is an internet connection before executing certain functions.

![]({{ site.baseurl }}/assets/images/HAVEX/058.png)

![]({{ site.baseurl }}/assets/images/HAVEX/059.png)

### 5.7.1 DNS Requests


Domain  | Type| IP                    
 ----------------- | ---------------------------- | ------------------
sinfulcelebs.freesexycomics.com  |   A   |   198.63.208.206
rapidecharge.gigfa.com  | A |   185.27.134.100

### 5.7.2 HTTP Requests

PORT  | Hostname| Path                    
 ----------------- | ---------------------------- | ------------------
80 |   sinfulcelebs.freesexycomics.com  |  /wp05/wp-admin/includes/tmp/tmp.php id=49321511259132175120161FD80c8a7af419640516616c342b13efab&v1=043&v2=170393861&q=45474b a5c3a10c8e94e56543c2bd
80 |   rapidecharge.gigfa.com       |      /blogs/wp-content/plugins/buddypress/bp-settings/bp-settings-src.php?id=49321511259132175120161FD80 c8a7af419640516616c342b13efab&v1=043&v2=170393861&q=45474bca5c3a10c8e94e56543c2bd


## 5.8 Process information

![]({{ site.baseurl }}/assets/images/HAVEX/060.png)

### 5.8.1 Evasion

* Checks for debuggers.

* Deletes activity traces.

### 5.8.2 Information collected

* Gets user name information.
 
* Gets computer name.
 
* Checks if user is admin.
 
* Uses a pipe for inter-process communication.
 
* Enumerates running processes.

If it detects Remote Access connections then opens a service named “TAPISRV” to force the user to enter credentials.

### 5.8.3 Mutexes


- CTF.LBES.MutexDefaultS-1-5-21-789336058-436374069-1343024091-1003
- CTF.Compart.MutexDefaultS-1-5-21-789336058-436374069-1343024091-1003
- CTF.Asm.MutexDefaultS-1-5-21-789336058-436374069-1343024091-1003 
- CTF.Layouts.MutexDefaultS-1-5-21-789336058-436374069-1343024091-1003
- CTF.TMD.MutexDefaultS-1-5-21-789336058-436374069-1343024091-1003
- CTF.TimListCache.FMPDefaultS-1-5-21-789336058-436374069-1343024091-1003MUTEX.DefaultS-1-5-21-789336058-436374069-1343024091-1003
- _!MSFTHISTORY!_
- c:!documents and settings!sandbox!configuración local!archivos
- temporales de internet!content.ie5!
- c:!documents and settings!sandbox!cookies!
- c:!documents and settings!sandbox!configuración
- local!historial!history.ie5!
- ZonesCounterMutex
- MSCTF.Shared.MUTEX.AJI (RAS related)

# 6.- Conclusions

We face a threat that, in this case was intended to be installed in industrial environments. It was observed that there have been different versions, which have been refined over time. At this point it can be considered that it has matured enough to carry out the theft of sensitive information from industry organizations.

# 7.- Annex

## 7.1 Sample configuration

Inside the main dll, we can find the Havex configuration in the resources section. By using the PeStudio tool, we get the resource doing a dump of that section.

![]({{ site.baseurl }}/assets/images/HAVEX/061.png)

The result is bzip2 file which contains encrypted data.

![]({{ site.baseurl }}/assets/images/HAVEX/062.png)

After decompression, we can decrypt the file using the decryptResource.py script (Annex). This script creates a new file named `% file% .decode`

    ~/virus/Havex$ python decodeResuocer.py setting

Then using the strings command we can see the configuration:

    ~/virus/Havex$ strings -e l setting.decode

## 7.2 Results
--------

MTMxMjMxMg==                                                          
base64(1312312)  

Havex                                                                 
name

14400000                                                              
unknown

Explorer.EXE                                                          
Process in which is injected

sinfulcelebs.freesexycomics.com/wp05/wp-admin/includes/tmp/tmp.php
rapidecharge.gigfa.com/blogs/wp-content/plugins/buddypress/bp-settings/bp-settings-src.php
C&C URLs

AATXn+MiwLu+xCoMG7SqY1uQxAk1qLdyoED9LxIVQr2Z/gsrHIsgTvK9AusdFo+9fzAxf1zXj42880+kUmktmVb5HSYi8 27Q54eQ4ZLUFKPKZstgHcwPVHGdwpmmRmk09fL3KGd9SqR60Mv7QtJ4VwGDqrzOja+Ml4SI7e60C4qDQAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAB
Public key

c8a7af419640516616c342b13efab                                         
unknown

45474bca5c3a10c8e94e56543c2bd                                         
unknown

600000                                                                
unknown

2000                                                                  
unknown

323000                                                                
unknown

svcprocess                                                            
Installation filename (svcprocess+043.dll)

## 7.3 C&C Servers 

Name  | Address| Host Name | IP | Country                     
 ----------------- | ---------------------------- | ------------------
 freesexycomics.com|  198.63.208.206|  x-screensaver.com| 198.63.208.206| United States 
 gigfa.com| 209.51.192.246| f6.c0.33.static.xlhost.com| 209.51.192.246 | United States


## 7.4 Panel Analysis 

The panel is located at: 

hxxp://sinfulcelebs.freesexycomics.com/wp05/wp-admin/includes/tmp/

We can see the reported files: 

- 13277210503045816459002FFD18-c8a7af419640516616c342b13efab.ans 
- 3818240600384801751700ACF830-c8a7af419640516616c342b13efab.ans
- 2152223526142981681400EEFD80-c8a7af419640516616c342b13efab.ans
- 425788980415205193170035FD58-c8a7af419640516616c342b13efab.ans
- 3332619927293187450087FA50-c8a7af419640516616c342b13efab.ans

We also found a password protected shell:

- hxxp://sinfulcelebs.freesexycomics.com/wp05/wp-admin/includes/tmp/tfdl.php

The other panel is located at:

- hxxp://rapidecharge.gigfa.com/blogs/wp-content/plugins/buddypress/bp-settings/

This are some of the the reports:

![]({{ site.baseurl }}/assets/images/HAVEX/063.png)

Havex uses 2 PHP files: one of them is the admin console, the other is the report collector.

### 7.4.1 C&C Panel

This panel verifies the user & password, and also adds the password in session.

The password is hashed with md5.

![]({{ site.baseurl }}/assets/images/HAVEX/064.png)

Analysis of C&C commands:

**vx command**

![]({{ site.baseurl }}/assets/images/HAVEX/065.png)

**new command**

Generates a new file containing the logs

![]({{ site.baseurl }}/assets/images/HAVEX/066.png)

**hash command**

This command receives the filename y return the md5.

![]({{ site.baseurl }}/assets/images/HAVEX/067.png)

**download command**

This command is used to download files.

![]({{ site.baseurl }}/assets/images/HAVEX/068.png)

**delete command**

This command is used to delete files.

**newans command**

![]({{ site.baseurl }}/assets/images/HAVEX/069.png)

**list command**

This command lists a directory.

![]({{ site.baseurl }}/assets/images/HAVEX/070.png)

# 8.- Scripts

## 8.1 Configuration extractor

decryptResource.py

    #!/usr/bin/env python

    #=============================================================================
    #
    # File Name         : decryptResource.py
    # Author            : Guillermo Campillo Perez <guillermo.campillo@drainware.com>
    # Creation Date     : Jul 2014
    #
    #=============================================================================
    #
    # PRODUCT         : Havex Resource Decrypter
    # DEPENDANCE SYS. : sys, base64,Crypto
    #
    # —————————————————————————
    # This document is the property of Drainware: any 
    # part of it can be reproduced or transmitted.
    #
    # 2014, Drainware, Inc.
    # —————————————————————————
    #
    #=============================================================================

    import os
    import sys
    import base64
    from Crypto.Cipher import XOR

    def _read(file_name):
       try:
        file_ = open(file_name, 'rb')
        buffer_ = file_.read()
        ss = XOR.XORCipher('1312312')
        y = ''
        for j in buffer_:
            y+=ss.decrypt(j)
        file_restul = open(file_name+'.decode','wb')
        file_restul.write(y)
        print 'Good Job Mama!'
        raw_input()
       except Exception as e:
        print '![x]Error:',e

    if len(sys.argv) < 2:
       print '![-]Usage: '+sys.argv[0]+' '
    else:
       _read(sys.argv[1])