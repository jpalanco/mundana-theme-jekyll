---
title: "Drainware"
date: "2020-01-22"
image: assets/images/drainware-1.png
author: jpalanco
layout: post
tags: [ cloud, data loss prevention, dlp, drivers, endpoint, open source, windows ]
categories: [ Projects ]
---

Between 2011 and 2014 we  developed a Cloud Platform with DLP capabilities, **now in 2020 it is Open Source**. It was a very cool technology at that time, we used mongo, redis, rabbitmq, .. among other technologies. Most of the magic was inside the endpoint, written in C++.

The team was composed by:
- [Cristian Sandoval](https://www.linkedin.com/in/cenriquesz/){:target="_blank"}, 
- [Marco Lojo](https://www.linkedin.com/in/marcoantoniolojo/){:target="_blank"}, 
- [Antonio Moreno](https://www.linkedin.com/in/antonio-j-moreno-de-la-rosa-60ba0240/){:target="_blank"},
- among [others](https://www.linkedin.com/search/results/people/?keywords=drainware&origin=SWITCH_SEARCH_VERTICAL){:target="_blank"}

This product is able to identify data leaks in buffers like the clipboard, screenshot (OCR), ... monitor removable devices, network units, applications (minifilter driver), cloud apps (dropbox, one drive, google drive), printer (OCR), ...

It uses geolocation based on the SSIDs using google location services to track stolen devices or known when a device was located when the data leak was performed.

It also comes with a basic sandbox to freeze applications abused by exploits by detecting suspicious traces in memory like nop-sled, heap-spray, ....

One of the coolest features was the distributed search across all endpoints of the organization. It was possible to find files, emails, documents, ...

Another interesting feature is that the endpoint includes a PHP interpreter to run callbacks or create validators based in regular expressions, REST API calls or whatever you can imagine. It also uses ADS, ssdeep and several fun things you will find browsing into the code.

Promo video:

<iframe src="https://player.vimeo.com/video/69536755" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

**Now this project is opensource!**

# The code

You can download the source code at Github:

[https://github.com/drainware](https://github.com/drainware){:target="_blank"}

**DISCLAIRME**: Use the code under your own responsibility. This project is not maintained for a long time, so most of the dependencies are obsoletes and some of them vulnerable.

# Screencasts

Drainware Intro:

<iframe src="https://www.youtube-nocookie.com/embed/J85Gcbs7pJY" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

Drainware DLP:

<iframe src="https://www.youtube-nocookie.com/embed/HKW_0Cf-1Ng" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

DLP Storage:

<iframe src="https://www.youtube-nocookie.com/embed/ZbdCBj9GT7Q" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

DLP Custom rules:

<iframe src="https://www.youtube-nocookie.com/embed/rpzp_M4YJAI" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

 

 

 

# Manual

 

## Introduction

This manual is written either to be read sequentially the first time, or can be used as a reference guide. During this reading you can find notices in the following formats:

![Description: notas.jpg]({{ site.baseurl }}/assets/images/description-ttp-primariamed-files-wordpress-com-5.jpeg) **Annotations**: Concept clarifications

 **![Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-ttp-alfredoquiroz-files-wordpress-c-10.png) Important!:** Important concepts to keep in mind

![]({{ site.baseurl }}/assets/images/word-image-10.png) **Tip**: Tricks, shortcuts and other tips

### About Drainware

Drainware is a security platform that is like a service. It has several modules to protect the information and/or the computers that contain this information.

We offer Freemium license which means you can start using it for free with some restrictions in its features.

## Requirements

### Operating System

Drainware can be deployed on computers with Microsoft Windows OS installed. The currently supported versions are the following:

|OS|Architecture|
|--- |--- |
|Windows XP|x86|
|Windows 7/8|x86/x64|
|Windows 10|x86/x64|


 **![Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-ttp-alfredoquiroz-files-wordpress-c-12.png) Important!**

Windows XP is supported only with Service Pack 3 or later. We also have support for Windows XP SP2, but you have to install the following components:

[Windows Search 4.0 for Windows XP (KB940157)](http://www.microsoft.com/en-us/download/details.aspx?id=23){:target="_blank"}

[Wireless LAN API (KB918997)](http://www.microsoft.com/en-us/download/details.aspx?id=2098){:target="_blank"}

- Minimum Hardware
  - CPU: Intel Pentium III 1 GHz or faster
  - RAM: 1 GB (2GB recommended)
  - HDD: 200 MB

## Installation

### Signing up in the system

Before installing Drainware, it’s necessary to have an account on the platform. To sign up in the system you’ll have to go to the official Drainware website at [https://www.drainware.com](https://www.drainware.com) and click on the _sign-up_ button in the top-right menu.

 

![home]({{ site.baseurl }}/assets/images/home-3.png)

![register]({{ site.baseurl }}/assets/images/register-3.png)

This will show us a form where we must input the information requested: registry data, company name, VAT ID, and the number of employees.

The e-mail will be associated with your account and it won’t be able to be changed in the future.

For the number of employees field, we only have to consider the ones that normally work with a computer.

 **![Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-ttp-alfredoquiroz-files-wordpress-c-13.png) Important!:** The password must have at least 8 characters.

Afterward, you will receive an e-mail that will allow you to validate your new account.

![register_mail]({{ site.baseurl }}/assets/images/register_mail-3.png)

When the license has been validated, it will redirect us to the sign-in page where we will have to input the e-mail and the password that we have entered in before.

![login]({{ site.baseurl }}/assets/images/login-3.png)

### Software endpoint installation

Once we have the license validated and entered our credentials, we are correctly signed in and able to download the software. After sign in, we have the possibility to download the installer. To the right of the download link, we have the license number that is a 16 digit code that we will need during the installation.

![Download]({{ site.baseurl }}/assets/images/download-3.png)

This installer will install the 32 or 64-bit version, depending on the operative system used.

### Advanced Installation

It is possible to deploy the endpoint in an unattended manner. This is very useful if you have a lot of users and you want to deploy it on a mass scale.

To do that, you can find the .msi installers available in http://update.drainware.com/ (Not any more here, go to Github)

The procedure to install it through the command line is below (where you must replace the red text by your license number):

```
msiexec /i file.msi /quiet /noreboot DDI\_LIC=XXXX-XXXX-XXXX-XXXX
```

If you prefer you can use this logon script:

Name: drainware\_logon.vbs

```vb
Function GetWindowsArchitecture(strComputerName)

Set objWMI = GetObject("winmgmts://" & strComputerName & "/root/cimv2")

Set colItems = objWMI.ExecQuery("Select \* from Win32\_OperatingSystem", , 48)

For Each objItem In colItems

GetWindowsArchitecture = "32-bit"

If left(objItem.Version,3) >= 6.0 Then

GetWindowsArchitecture = objItem.OSArchitecture

End If

Next

End Function

Function GetProgramsFolder()

Set wshShell = WScript.CreateObject("WScript.Shell")

GetProgramsFolder = wshShell.ExpandEnvironmentStrings("%programfiles%")

End Function

Function ExistDrainwareSecurityDir()

Set objFSO = CreateObject("Scripting.FileSystemObject")

ExistDrainwareSecurityDir = objFSO.FileExists(GetProgramsFolder() & "\\Drainware\\Drainware Security Endpoint\\DrainwareSecurityAgent.exe")

End Function

Function DownloadDSE(strRemoteDSE, strLocalDir)

Set objFSO = CreateObject("Scripting.FileSystemObject")

objFSO.CopyFile strRemoteDSE, strLocalDir & "\\"

End Function

Function InstallDSE(strLicense, strRepository)

If Not ExistDrainwareSecurityDir() Then

Set wshShell = WScript.CreateObject("WScript.Shell")

Select Case GetWindowsArchitecture(".")

Case "64-bit"

Rem Msgbox "Installing Endpoint 64-bit " & strLicense

strRemoteDSE = strRepository & "\\SetupCloud.msi"

strLocalDSE = wshShell.ExpandEnvironmentStrings("%temp%") & "\\SetupCloud.msi"

Case "32-bit"

Rem Msgbox "Installing Endpoint 32-bit " & strLicense

strRemoteDSE = strRepository & "\\SetupCloud32.msi"

strLocalDSE = wshShell.ExpandEnvironmentStrings("%temp%") & "\\SetupCloud32.msi"

End Select

DownloadDSE strRemoteDSE, wshShell.ExpandEnvironmentStrings("%temp%")

Rem Msgbox "msiexec /qn /i " & strLocalDSE & " ddi\_lic=" & strLicense

Rem WshShell.Run "msiexec /qn /i " & strLocalDSE & " ddi\_lic=" & strLicense

Msgbox "Your computer will restart after a few seconds"

End If

End Function

Dim strLicense

Dim strRepository

strLicense = WScript.Arguments(0)

strRepository = WScript.Arguments(1)

InstallDSE strLicense, strRepository
```
 

Usage:

```
drainware\_logon.vbs LICENSE LOCATION
```

example: 

```
drainware\_logon.vbs XXXX-XXXX-XXXX-XXXX \\\\mynas\\resources\\dlp\\
```

The location must contains both msi files (for x86 and x64)

**Useful links**

[Create a GPO (Windows 2008](http://technet.microsoft.com/en-us/library/cc754740.aspx)){:target="_blank"}

## Initial configuration

In this section, we will go through the initial configuration of Drainware. These are the available options in the left menu (red area) of Drainware once you sign in.

![menu]({{ site.baseurl }}/assets/images/menu-3.png)

### Credentials

In this section, we can update our password. If we want to change it, we also have to fill in the current password.

![credentials]({{ site.baseurl }}/assets/images/credentials-3.png)

### Subscription

Drainware has two different subscription types. One is the Freemium option, which offers a monthly service with a limit of 500 security events; after 500 events, the organization will be unprotected until the first day of the next month.

On the other hand, we offer a Premium subscription that is based on the number of users you wish to protect. The Premium subscription includes unlimited events (as long as use remains reasonable).

In this section, it is possible to check the validity of the subscription and upgrade it in the case of using a Freemium subscription.


### Groups

It is possible that in your organization you would like to apply different policies depending on groups of users. We can organize the groups by areas or departments, depending on the requirements of the organization.

In this section, we can create the groups inside our platform and then apply policies directly over them.

It is possible to integrate the groups in the organization directly with Drainware, and this topic is explained in more detail in section 4.5.

### Users

Every time that user logs in to a computer protected with Drainware, the server is notified, and it will register it in the system. From that moment, we can associate that user to one or more groups.

### Authentication

To integrate Drainware with your organization, we offer an authentication module. We have 2 different options to configure the authentication module: local authentication or LDAP.

By default, Drainware works in the local authentication mode, in such a way that the group information is already in our platform.

With the LDAP option, it’s possible to integrate an LDAP server or Active Directory Domain to be able to use the users and groups of the organization.

If you want to integrate LDAP, it’s necessary to open the LDAP port to the Internet. We recommend opening it with SSL exclusively.

If you want to integrate it with Active Directory, you should use the following information:


|Field|Value|
|--- |--- |
|Type|LDAP|
|SSL|Depending on your configuration|
|Version|2.0|
|Host|IP or Computer Name|
|Port|389 or 636 if it’s SSL|
|DN|DOMAIN\User|
|Password|User Password|
|Base|DC=DOMAIN, DC=LOCAL|
|User Attr|sAMAccountName|
|Recursive Groups|Optional|


We recommend to use always LDAP with SSL and to block any connection except if it comes from our public IP Adress.

We also have the “Recursive Groups” option. This option allows users in nested groups to resolve the groups to which they don’t directly belong.

![Description: notas.jpg]({{ site.baseurl }}/assets/images/description-ttp-primariamed-files-wordpress-com-7.jpeg) **Annotation**: If an LDAP user doesn’t belong to any of the imported groups, it will belong to the default group automatically.

 **![Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-ttp-alfredoquiroz-files-wordpress-c-15.png) Important!:**

When the LDAP is integrated, all users will be available in the platform however the same doesn’t happen with the groups. The groups must be imported one by one from the group's section, which will also be integrated with LDAP.

### Time Zone

It’s possible that the employees of an organization work or travel around the world. Therefore, in Drainware, we work with the UTC time zone. In order to translate the time between different time zones, we offer the possibility to select the time zone where the administrator wishes to see the events.

## Dashboard

The main window of Drainware shows an overview of the security events that happened since the installation of Drainware. It also shows the details of the events that happened since the beginning of every month.

![dashboard.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktopdashboard-png-3.png)

For Freemium users, it shows a status bar that shows the monthly events. When the number of events reaches 500, Drainware will stop working until the beginning of the next month. The administrator will then receive an e-mail notification that the organization is not protected with Drainware anymore.

![]({{ site.baseurl }}/assets/images/word-image-13.png) **Tip**:

To the right of the monthly events bar, you can find a link to get more free events per month in the Freemium version. To receive more free events, you only have to share a link with the reference code. For every verified installation referred to this code, Drainware will give you 100 extra free events per month.

## DLP

In the DLP module (Data Loss Prevention), we can control the confidential information inside the organization to prevent data leaks.

![menu_dlp.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktopmenu_dlp-png-3.png)

### Policies

The policies define what information you want to monitor and what action will be carried out. In the policies creation section, we provide a wizard that makes the whole process easier. We’re going to create a policy with the name POL001 and the description of “_Policy 1”._

![pol1.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol1-png-3.png)

In the first step we have to provide a name and a short description of the policy:

![pol2.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol2-png-3.png)

In the next step, we have to define the information that we want to protect.

We can see the next menu:

- Concepts / Subconcepts: patterns predefined by Drainware to identify the information.
- Applications: applications that we’ll deny any access to confidential information.

As we continue configuring Drainware, this section will contain other elements such as rules, files, and network sites; which will see in the next sections.

![pol3.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol3-png-3.png)

If we expand the Concepts/Subconcepts we will see a big list of categories. We can include a subconcept in our policy like Visa or the credit card concept that would include all credit card types.

![pol4.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol4-png-3.png)

In the applications section, we can see a list (that can be extended by the user) that allows the blocking of several programs.

![pol5.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol5-png-3.png)

In Step 3 we can see a list of the groups that we have already imported, the action that will be carried out, and the severity (how severe is the group of users that triggered the policy).

![pol6.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol6-png-3.png)

We only have to select the groups that we want to be affected by the policy. When defining the action, it can be:

- Log: logs the event in the Drainware database for audit purposes.
- Alert: an e-mail is sent by default to the e-mail address used for sign up in Drainware, but it can be overridden by another address specified only for this policy.
- Block: prevents filtering of information.

In all cases, the employee that executes the policy will see a notification.

![pol7.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol7-png-3.png)

We only have to click the “Finalize” button and the policy will be created.

![pol8.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol8-png-3.png)

Every time we create a policy, it will appear in the policies list. In this list, we have 3 buttons:

- Configuration: we can configure the information to protect, like we configured in step 2.
- Action: we can re-define actions for the different groups, like we configured in step 3.
- Remove: removes the policy.

Once the policy is created, it can’t be renamed.

![pol9.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoppol9-png-3.png)

### Rules

With “Rules”, we can define our own information patterns to protect inside the policies. We can include, for example, confidential footers that we usually introduce in documents with confidential information. We can also add regular expressions that describe any confidential documents that we want to protect.

To create a rule, we have to introduce a name without spaces and special characters (A), a description (B), optionally, we can include a verification function in PHP (C) and we can define which policies we want to associate with this rule (D). Like policies, rules can’t be renamed either.

![]({{ site.baseurl }}/assets/images/word-image-15.png) **Tip**:

If we want to use a verification function in PHP, it will receive the variable “$match” that contains the resulting match after the regular expression is applied. It will be necessary that after analyzing $match, it will assign TRUE (accept match) or FALSE (deny match) to the “$return\_val” variable.

![rule.png]({{ site.baseurl }}/assets/images/macintosh-hdusersjosedesktoprule-png-3.png)

### Files

For very exceptional cases, it’s possible that a rule can’t cover all our requirements and we’d want to sign up for a file. In these cases, we can upload a file to help Drainware to identify when someone is trying to filter information.

The procedure is very simple. We can upload one or more files and they will be automatically available to associate with our policies. We only have to go to the policy configuration and select the filename.

Every time we upload a file, this will be available in the new policies wizard.

![Description: files.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopfiles-3.png)

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-20.png) Important!:**

Before uploading a file, we suggest to use a unique filename or even put the current date to distinguish it from another with the same name.

 

### Network Sites

In the network sites section, we can add Windows shared folders with the format \\\\server\\resource.

This functionality is one of the most interesting ones. The endpoint software is ready to identify all the files copied in a computer from the shared folder added in Drainware. Once the file is copied, Drainware will check every file or every copy of them throughout the computer’s file system, allowing you to work with it, but denying its filtration.

For Network URI, we have to input the shared folder location., We must also introduce a short description, and then select the different policies to apply.

It will be available in the new policies wizard.

![Description: network place.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopnetwo-5.png)

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-21.png) Important!:**

Only files that have been copied after add the shared folder will be monitored.

 

### Applications

To add more applications and include them in our policies, we can add them in the “Manage Applications” section.

To add a new application, we will need its name, for example, iexplorer.exe, or skype.exe. Similarly to the other sections, we have to put a short description and select the policies to associate with it. It will be available in the new policies wizard.

![Description: apps.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopapps-1-3.png)

### Advanced

![Description: block_crypt.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopblock-3.png) In the Advanced section of Drainware, we can configure the behavior of the DLP. We have 3 sections to configure its behavior.

The first section will allow us to block access to encrypted information within particular groups. The behavior will be the same as a file affected by blocked policy.

![Description: evidence.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopevide-3.png)

The second section will allow us to collect evidence every time an event is carried out. This configuration is directly related to an action defined in the policy, where we can define a criticality level for each group. In this configuration, we can select ‘None’ if we don’t want to collect evidence or the minimum level from which we would want to make for the collection. If we select the low level, the collection will be available for the low, medium, and high levels. If we select the medium level, it will be available only for the medium and high levels. And if we select high, it will be available only for that level.

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-22.png) Important!:**

The configuration of the evidence collector is only available for the Premium users. The Freemium users will receive the first 3 screenshots every month.

 

In the last section, we can globally enable or disable modules that affect all policies. In Drainware we consider 3 types of elements:

- Source: information origin
- Sink: information destination
- Pipe: information channel

![Description: dlp_advanced.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopdlp_a-3.png)

In sources, we currently only have “Network device”. That allows us to recognize Windows shared folders. If we disable this origin, the “Network Sites” section will stop working and it won’t be visible in the menu anymore.

In Sinks we have several modules that monitor the application of the corresponding action (block, alert or log):

- Dropbox
- Skydrive
- Google Drive
- Network Device
- Pendrive
- Printer

Finally, in Pipes we can monitor:

- Clipboard Image
- Clipboard Text
- Keylogger

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-23.png) Important!:**

The keylogger module doesn’t allow block the tipping, because until it isn’t written it can’t be analyzed.

 

### Notifications

Notifications can’t be configured in the DLP menu, they must be defined in the “General” section, but they are directly related to the DLP.

The notifications allow, as long as we have a browser opened and logged in, the receiving of notifications in real-time when an event is carried out.

We don’t recommend enabling the notifications for all actions and events, because, if they are executed regularly, it can be annoying.

The notifications are HTML5 notifications and they are integrated with the desktop of the operating system, as long as the browser and the operating system support it.

![Description: notifications.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopnotif-3.png)

## Sandbox

The Sandbox feature allows us to protect applications against virus. It’s not an antivirus replacement, but rather, a complement.

![Description: menu_sandbox.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopmenu_-8.png)

Previously, hackers took advantage of security problems in the server’s software to gain access to the organization. But a security suite was developed to enable firewalls, IDS, IPS…

In the last few years, hackers have taken advantage of new vectors. Using tools like LinkedIn, they can discover who a financially responsible person is, and what contacts he has. From that moment they can make an attack based on spear-phishing that consists of sent e-mails assuming his identity with an attached PDF or an URL that steals data or opens a connection to the outside.

### Applications

In Drainware, we develop rules that allow us to block the affected applications before the system will be affected.

![Description: sandbox.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopsandb-5.png)

## Inspector

With the Inspector module, you can search in real-time over all the computers in the organization.

![Description: menu_inspector.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopmenu_-9.png)

It’s possible that in the organization we have a person or a group of people working with the kind of information to which they shouldn’t have access. It could be done unconsciously or premeditated. Either way, we can find out with the Inspector tool.

Furthermore, once we have experienced a leak of information, it is often very difficult to check all the computers where the related document was. With Inspector, it is possible in seconds, to find very specific files, download them, and even browse through the file system of the computers affected.

### Remote search

With the remote search we can start to obtain results.

![Description: search_result.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopsearc-3.png)

The search can take several minutes. The results are shown grouped by the name of the computer where the file was found. Expanding the results by computer, it’s possible to see the file details by clicking on it. We can see information about the modification date, file name, mime type, creation date, and short information about the file header. It’s also possible to download it.

![Description: details.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopdetai-3.png)

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-27.png) Important!:**

You shouldn’t search by very short terms or generic terms. The result can take too much time or it can be [unmanageable](http://www.wordreference.com/es/translation.asp?tranword=unmanageable).

 

It’s possible to browse through one of the computers listed in the results. To do this, you must click on the computer name or IP address (red area).

![Description: browse.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopbrows-6.png)

The file explorer feature is further detailed in section 7.3 of this manual.

### Multiple Remote Searches

If we want to search for a lot of terms, it’s possible to use the Multiple Remote Searches function.

To use this feature, you have to create a file with all the search terms in one line, separated by commas. We can create different lines, each one with its own keywords.

keyWordGroupA-1, keyWordGroupA-2, keyWordGroupA-3

keyWordGroupB-1, keyWordGroupB-2

keyWordGroupC-1, keyWordGroupC-2, keyWordGroupC-3

The file extension must be TXT. In addition to uploading the file, we must input a name for this report.

![Description: multiple.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopmulti-3.png)

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-29.png) Important!:**

You shouldn’t search for very short terms or generic terms. The results can take too much time to obtain, or the results can be [unmanageable](http://www.wordreference.com/es/translation.asp?tranword=unmanageable).

 

### Remote Files explorer

The Remote Files Explorer allows us to inspect any computer in the organization with Drainware installed.

We will have to provide some details about the computer: computer name, IP address, and optionally, the path. From this point, we can browse through any device in the computer and even download files.

![Description: browse_details.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopbrows-7.png)

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-30.png) Important!:**

Drainware is not developed to be an FTP server. Downloading a file with several MB in size can take several minutes until the download starts.

### Remote Devices

With this feature, we can see the geographic position of all the devices that have Drainware installed.

In most cases, the geolocation is performed through the IP address, but when the Wi-Fi is activated, it’s possible that the geolocation is performed through Wi-Fi triangulation.

![Description: inspector_map.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopinspe-3.png)

 **![Description: Description: aviso_importante1.png]({{ site.baseurl }}/assets/images/description-description-ttp-alfredoquiroz-file-31.png) Important!:**

Make sure that you don’t refresh the webpage until all the endpoints have responded, especially in networks with thousands of endpoints, as the webpage loading could take several minutes.

In addition to the geolocation of the devices, it’s possible to get a network map encapsulating all the computers that belong to the same ranges. To that effect, we will click on the Network View tab.

![Description: Screen Shot 2013-11-19 at 14.59.29.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopscree-3.png)

The results are shown in circles, where every circle represents a range or a group of ranges.

![Description: network-1.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopnetwo-10.png)

![Description: network3.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopnetwo-11.png) It’s possible to click on the segments that we want to inspect and see all the computers connected at that moment.

## Reporter

With the Reporter module, we can have access to the data recorded by Drainware. We can get details of every module or statistic from the global behavior of the DLP, Inspector, or Sandbox.

![Description: menu_reporter.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopmenu_-11.png)

### DLP Events

Once we open the DLP events information, we can see a graph with all the events related to the data leak. Under the graph, we can see a table with a list of related events, ordered from the most recent to the oldest. The table has some controls at the bottom where we can refresh it or browse through.

![Description: DLP.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopdlp-p-3.png)

The list only shows a preview of the event. If we want to see detailed information, we must click on it.

The details of each event are shown in a table that provides all the information related to the event. Depending on the configuration, it’s also possible to see a screenshot done at the same moment that the event was carried out.

![Description: DLP_events.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopdlp_e-3.png)

![Description: Description: notas.jpg]({{ site.baseurl }}/assets/images/description-description-ttp-primariamed-files-1-3.jpeg) **Annotations**: Freemium users can only see the first 3 screenshots every month.

Under the table, there is a button which generates a report with the latest security events.

![Description: export.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopexpor-6.png)

If we want to find events by a range of dates, event type, policy, severity, rule, etc., we can use the “Advanced Query” system. As we can have a result with too many events, it’s possible to fill in the maximum number of events we want to show in the result.

![Description: DLP_reporter_Search.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopdlp_r-6.png)

Every time a query is generated, it’s possible to export the results in CSV format. In order to do this, you have to click on the Generate Report button at the end of the page:

![Description: export.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopexpor-7.png)

### DLP Stats

The events and detail of events information is interesting, but in many cases, it’s necessary to have a view at a higher level of what is happening with confidential information or to know how the policies that we have configured are working. To do so, we will create data analysis and statistics.

#### Activity

In the same graph, it represents the average between severity, action, and the number of events. The policies with more events are located to the right, with the vertical axis representing the average of the actions carried out, where the block is the highest part. The average of the severity is shown in the size of the circle. In the top left combo box, you can select the period of time.

![Description: dlp_report.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopdlp_r-7.png)

#### Groups by policy

In this graph we can see the groups that carried out more events of one policy. In the top left combo box, you can select a period of time. In the top right combo box, you can select the policy.

![Description: group_by_policy.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopgroup-6.png)

#### Users by policy

In this graph, we can see the users that carried out more events of one policy. In the top left combo box, you can select a period of time. In the top right combo box, you can select the policy.

![Description: user_by_policy.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopuser_-3.png)

#### Policy

With the policy graph, we can analyze the policies with more activity. In the top left combo box, you can select the period of time.

![Description: policy.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktoppolic-3.png)

#### Groups

With the policy graph we can analyze the groups with more activity. In the top left combo box, you can select the period of time.

![Description: group.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopgroup-7.png)

### Sandbox Events

We can see a graph with related events with attempts to abuse applications. Under the graph, we can see a table with the list of events, ordered from the most recent to the oldest. The table has some controls at the bottom where we can refresh it or browse through.

### Sandbox Stats

#### Applications

With the applications graph, we can analyze the policies with more activity. In the top left combo box, you can select the period of time.

![Description: sandbox_apps.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopsandb-10.png)

#### Groups

With the policy graph, we can analyze the groups with more activity. In the top left combo box, you can select the period of time.

![Description: sandbox_groups.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktopsandb-11.png)

## Inspector search reports

When we make multiple remote searches from the Inspector section, the results are generated in this section. We can find the report by a range of dates to download in Microsoft Excel format.

![Description: reporter_inspector.png]({{ site.baseurl }}/assets/images/description-macintosh-hdusersjosedesktoprepor-3.png)

## Troubleshooting

### Corporate Proxy

Drainware supports connection through a proxy, either configured in the system or auto-configured. However, if the proxy uses authentication, it’s necessary to enable “\*.drainware.com” in the accessible domains without authentication.

If you are using SQUID, the configuration would be the next one:

acl drainware dstdomain .drainware.com

acl CONNECT method CONNECT

acl dwCONNECT dstdomain .drainware.com

http\_access allow CONNECT dwCONNECT localnet

http\_access allow drainware localnet
