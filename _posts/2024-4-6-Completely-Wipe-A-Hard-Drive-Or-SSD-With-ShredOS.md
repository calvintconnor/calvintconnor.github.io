---
title: "Completely Wipe Any Hard Drive or SSD with ShredOS"
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
  - Tutorials
tags:
  - cybersecurity
---

If you don’t know the difference between formatting a hard drive versus running ShredOS, then this article is for you. ShredOS, in simple terms, can replace every bit of a hard drive with either ones or zeros. After running shredOS, nwipe has erased absolutely everything, including the operating system, data, partition table, and file system. Only specialized programs can recognize it after this. If you are looking for a tool to make any data on a drive completely unrecognizable, then you have found the right one.


## What Does It Actually Do?
There are several options that you can instruct ShredOS to apply to the data on your hard drive. You can have it replace everything with 1s or 0s, random strings of data, or do all of this multiple times in different orders. The goal is to replace every bit on your hard drive, used or not, with arbitrary values so no real data can ever be recovered from it. If you did not know, this is a huge difference from just having Windows format your drive for you. 

## How To Run It?
ShredOS is built to run on a bootable thumb drive. This allows you to plug it into any computer and start using the utility instantly. You can checkout the official github here https://github.com/PartialVolume/shredos.x86_64 to gain official info as it may get updated from time to time. Once you boot into into ShredOS you will be presented with a simple GUI where you can select your drives, choose what wiping methods with how many layers, and finally begin wiping by hitting Shift + s. Depending on what you selected this can take quite a few hours to fully fill the drive, especially if it is an older hard drive. In my line of work we go with three different wiping techniques for older hard drives which ends up meaning they will be finished overnight. Do not expect this to only take a few minutes. A warning from someone who has previously made this mistake: do not select your operating system hard drive if you are running shredOS on a good computer as your internal drive will appear and can be wiped as well.

## Errors
If you get some kind of error and you really need the data erased the best thing to do is make sure the drive is properly seated and powered on and run the wipe once again. After that, I really hope you have a drill press.

## Conclusion
As always, I am just some random guy on the internet telling you what to do with your data. Do your own research, investigate other tools, and you will still end up coming back to ShredOS as I did. The difference being you now know it is the right choice. Hopefully this article was able to put an extremely helpful tool on your radar.


