---
title: "FTP (File Transer Protocol) For Beginner Penetration Testers"
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
  - FTP
---

FTP stands for File Transfer Protocol, and in case you can’t figure that out it allows you to upload/download files. While FTP does have different versions with some exploits it is so rare to find these that rather this post focuses on what you need to try when you are up against FTP that is not obvious for the beginning penetration tester.

## Connecting
While doing a nmap scan you might see port 21 showing up. You should burn this into your brain as FTP, as unlike SSH, FTP is 99.99% of the time on port 21. To connect to FTP from Kali Linux you can simply run the following commands.

```
ftp 192.168.1.1
nc 192.168.1.1 21
```

The ftp command is my preferred as it has a cleaner interface, but for nc works in a pinch. In almost all scenarios FTP will prompt or wait for you to enter credentials. Even if anonymous FTP has been enabled you still have to enter the anonymous:anonymous credentials (representing the username and password separated by a :). If you have no other info for possible credentials you should always try: root:root, admin:admin, ftp:ftp, nameofbox:nameofbox, and themed words popping up in the engagement. Too often I banged my head against the wall as a beginner just to finally give in, look up the answer, and realize the password was just the name of the box. Use your intuition, people set awful passwords and even real life something like john:password happens way too often. Do not assume just because it is a service that you cannot guess the password. While there are tools that let you brute force FTP logins, this is rarely the answer unless something has given you a hint to.

## Commands
As a beginner it is helpful to type “help” upon connecting to the ftp service for the first few times. This will allow you to become familiar with the commands available to you before you no longer need to. Maily, we are looking for if we have permissions to upload, download, or both. You can also test this by simply trying to upload or download a file. This can give you a great clue as to what your next steps should be. This may sound dumb at first, but don’t get confused just because you are in an unfamiliar screen. FTP is just showing you a folder on a computer designated to be shared with FTP so permissions and everything else that comes with files still applies. 

A common scenario you might face is a box running a web server where the FTP folder shared correlates to a directory on the website. The step here is to upload a webshell or executable and run it by opening it with the website. This leads us to the ASCII vs Binary confusion that can cause hours of frustration. ASCII and Binary modes change how your files are uploaded in FTP and in many cases can break what you are trying to do if you are in the wrong mode. You should be in ASCII mode, simply by typing ascii, to upload text files. To upload .exe, .zip, .tar, .z, .gz, and graphical files you should be in binary mode, which you can enter by typing binary. If you did not know this was a thing, trust me I just saved you a lot of confusion when your shell is not working.

## Methodology
Often in an engagement the angle is to use some info contained in a file in FTP to further access. Do not forget your upload capabilities when a service like a website is running. In some scenarios it may be as simple as checking help to see you have access to a command that instantly gives you a shell. If you ran your nmap scans properly you should see all the version information available. If it looks extremely old, which you will get a feel for, it might be worth digging into the specific version. Otherwise, do not forget you have access to a sensitive shared folder – information found should not be taken lightly.

## Conclusion
If you know when to use ASCII vs binary, what to enter to log into FTP anonymously, and understand FTP is just shared files then you have everything you need to know. Often times FTP is used in a larger explot chain, but can still have its opportunities for direct code execution. Knowing the limits of a service is extremely useful as a beginner as you simply do not know what you do not know. I accept all criticism, so if you feel this post could be better for future readers feel free to give me everything you have by leaving a comment, emailing me, or any other forms of harassment.


