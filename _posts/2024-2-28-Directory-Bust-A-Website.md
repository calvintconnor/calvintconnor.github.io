---
title: "Directory Bust A Website With Feroxbuster"
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
  - Tools
tags:
  - cybersecurity
  - penetration testing
  - Hack The Box
  - HTB
---

This post has three headings depending on what information you need:
1. Gobuster is still good! is my thoughts on why feroxbuster is better, but only for certain things.
2. Getting Started is how to install and get up and running with commands to add to your notes.
3. How Is This Helpful? expands upon why I continue to look for new tools even when old ones still do the job.

## Gobuster is still good!

Before I discovered feroxbuster I was using dirbuster and gobuster for 99% of my engagements. To be honest, I could continue to use gobuster and dirbuster for most of my engagements with little performance and speed impact. Feroxbuster shines in how it displays its information, and while it does some fancy things behind the scenes to be faster, its unique ability is to display recursive dirbusting information in an easy to digest and visual way. Feroxbuster’s interface makes it easier to spot mistakes and errors in your URL, word list, and extensions than something like gobuster. It presents information in a way that does not clutter the screen while simultaneously displaying everything you need to know - in a real-time updated format. What you should not do is abandon every other dirbusting tool, thinking this is the tool to end all tools. For example, on a specific certification that shall not be named, it was only with gobuster that I was able to successfully understand errors being thrown at me with these dirbusting tools. That was vague and non-helpful on purpose. The takeaway is that a hacker needs multiple tools for every job, as one might not present the information he really needs during that engagement. Now that you understand feroxbuster will not start doing your laundry and do the hacking for you, let’s get right into how to use this thing.

## Getting Started

You can follow along and checkout their main GitHub page here: https://github.com/epi052/feroxbuster?tab=readme-ov-file. For the sake of keeping you in one place, I will streamline the installation and common use scenarios to record in your notes. If you’re using kali, this is the preferred install method. Installing from the repos adds a ferox-config.toml in /etc/feroxbuster/, adds command completion for bash, fish, and zsh, includes a man page entry, and installs feroxbuster itself.

```
sudo apt update && sudo apt install -y feroxbuster
```
At the base, run feroxbuster using the feroxbuster command and -u, --url, flag as seen below. This will automatically start a recursive dirbust with the default wordlist.

```
feroxbuster --url http://192.168.142.112/
```

to change the wordlist and file extensions, add the --wordlist and -x respectively.

```
feroxbuster --url http://192.168.142.112/ -x php,asp,aspx --wordlist /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
```

The only other helpful flag you need before you dive off into the real tutorial for more specific cases is the –burp flag to automatically proxy traffic to http://127.0.0.1:8080

## How Is This Helpful?
This is just another tool to add to your belt. I prefer it because I can more quickly understand what is going on compared to other tools, but it is important to have practiced all of them to use in any scenario you need. I thought I would make this post because during my journey through the OSCP and countless HTB tutorials, I never even heard of feroxbuster. It is a sleek, modern tool to add to your dirbusting arsenal. In times of panic, we go to what we know, so if you are preparing for your OSCP journey or making your way through the Hack The Box platform take this bit of advice from someone who has just travelled that path: practice so your notes become the second source of information, the first being your head.
