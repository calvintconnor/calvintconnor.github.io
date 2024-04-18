---
title: "OSCP: Everything You Need and Did Not Want To Know"
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
  - certification
tags:
  - cybersecurity
  - penetration testing
  - oscp
---

This post has three headings depending on what information you need:
1. My Journey is a recount of everything I have done in life to prepare for the OSCP.
2. The Down Low is everything you want to know about the exam: how it feels, what you need to be prepared for, and what to expect.
3. Now What? is my expanding on the OSCP and where and what it fails to teach you.



## My Journey

On a late night in November 2023, I officially passed the OSCP. Ten years before that, I was a child following YouTube tutorials to make my own web pages in HTML and CSS. But did I really need that start to make it to where I am now? The answer is no, and I also want to show you why or why not the OSCP is not really that hard. Yes, I was making websites since before I even really knew how the internet worked, but none of that prepared me for the exam I had just taken. You do not have to love technology and hacking your whole life to even be able to stand a chance against the OSCP. A word of caution, it will take more effort than you are accounting for. So where did I really begin?

Even though I had been making websites for forever, I was not that into technology. In fact, no one in my life recognized me as some kind of tech genius or encouraged me to go into this field. Because in my heart, I am not a tech junkie. I love learning; I always have, and I always will. That is what makes me so great at technology. I have an earnest desire and passion to understand everything about something. I am a tinkerer, a researcher, someone who spends countless hours going down rabbit hole after rabbit hole for what should have been a simple question. If you are on your OSCP journey, and you feel this way too, then it is a great sign. It is not a requirement, but the truth of what makes getting the OSCP an enjoyable experience versus a never-ending security nightmare.

My technical training for the OSCP began when I went off to college. I went to a local community college that cost me less than 10,000 dollars in total. I also knew when I went to college that I simply could not do four years, as I did not believe the time invested was worth it. So instead, I signed up for a dual major in cybersecurity and computer networking. Upon graduation, I received an associate in both.

My college classes consisted of A+, Cisco Networking Academy, Security+ networking topics and classes. My cybersecurity classes were very lax and often only covered broad topics, while my networking classes involved creating your own VLANs, diving into the OSI model, and understanding networking to its most rudimentary core. 

Shortly before completing my degrees, I secured my first job out of sheer luck for a local library as their Help Desk agent. This included answering the phone, emails, and in person meetings to answer and solve people’s technological questions. This help desk job rarely required the knowledge I had gathered in college. Luckily, the Network Admin there took me under his wing and started to show me the side of network administration and solutions in a real-world environment. It was quite refreshing to see everything you had learned in school played out for real business needs.

After almost two years of working there, I decided I not only needed a change of scenery, but that I wanted to do more. That is what set me onto what I now know is the OSCP and PNPT. Through a combination of reaching out to my previous cybersecurity teacher at college and a few late nights researching different fields I could go into, I finally decided on becoming a penetration tester. Everything I had researched, and the nudging of my teacher, told me this was the certification to get and strive for as someone who had no idea what they were doing. Before I decided to achieve the OSCP I had not completed a single box on HTB or any platform, nor did I know that was an option.

The OSCP is slightly higher than mid-level certification, and as a complete beginner, I knew I needed something a little more beginner. Through some research, and some particularly helpful Reddit threads, I found the PNPT certification from TCM Security. Not only was it a steal at a couple of hundred bucks compared to the OSCP, but it explained every topic from the ground up. Where the OSCP would expect you to already have Kali Linux installed and configured, the PNPT guided you through the installation and setup. This was extremely helpful as I had also never touched Linux before.

Over the next couple of months I progressed through the PNPT materials, often taking breaks to research other security topics, until I was ready to begin attempting hacking into my own boxes. I settled on Hack The Box as my subscription of choice and began progressing through TJ Null's list of boxes in the easiest order first. It was also in this time that I discovered IppSecs tutorials videos, for if it was not for, I would probably not be here today. Just by watching and taking notes on IppSecs videos I learned more about penetration testing than I did in the last month. From his hacking methodology to the way he simply explains obscure topics, his knowledge was an invaluable wealth to me.

At the same time, I also purchased the OSCP bundle to begin taking their training. After completing all the training materials and labs, accompanied by over fifty HTB boxes, I finally felt prepared to take the OSCP. It had just been about four months since I started, and I spent at least fifty hours a week working full-time just studying. For those wondering how I did that working, I did not. I quit my job with enough savings to last me six months. 

## The Down Low

As you probably already know, the OSCP consists of an Active Directory module and three standalone devices of either Windows or Linux machines. To pass you need to achieve at least 70/100 points with the AD module being valued at 40 and each standalone box being valued at 20 - ten for user and ten for root. This means that without the 10 bonus points you get for doing 80% of all exercise modules and at least 30 labs, you cannot pass without the AD module. Now that we know how to solve it, let's go over what resources you will need, depending on what level of competency you are at.

Beginner

If 192.168.1.1 and 256.4.0.643 mean the same thing to you, then you need to go back to networking basics. Even if they don't, if 10.5.5.0/24 also doesn't make sense, you still need to go back. Throughout the exam, it is given that you will be working with IP addresses to understand the network you are in. You will need to have an excellent understanding of IP addresses, a basic understanding of ports on a computer, and how operating systems work. If you feel you fit into this category of networking, then I encourage you to follow the path of the CCNA. The Cisco Certified Networking Associate is Cisco’s certification for networking. While it does involve a lot of Cisco equipment specifics, most of the information taught is universal and key for understanding all the information you will need on your journey. You do not necessarily need to take or purchase materials for the CCNA, as there are quite a few free resources and YouTube series out there. Once you can create your own subnet, know what port SSH runs on and what it is, know how a packet will be forwarded through a network, and create your own network in packet tracer, you are ready to move forward.

Intermediate

If you understand network concepts, have manually created a subnet, might have remoted into a machine or SSH, and installed Linux and played around with it, you might be ready for these resources. You are an intermediate if you can describe how information flows through a network, understand why a website may be unavailable, and know a few commands in cmd.exe like how to ping a computer or what to look for in ipconfig /all. While you have a lot of technology training, you probably have little to no security training; and that is what we need to fix. My path, and what I recommend, is to move through the resources of the PNPT by TCM Security. It is an entry level certification and at just a few hundred dollars its value is severely underpriced. You do not need to pass the PNPT, though I do recommend taking it once, as you get one free retake. I waited until after the OSCP to take the PNPT. The resources in the PNPT are incredibly valuable to someone who knows networking but needs someone to explain to them how to read python and install and move around Kali Linux for the first time.

Advanced

If you have done a few Hack The Box boxes with very minimal hints needed, actively enjoy and slightly understand IppSecs videos, and have messed around and created a few beginner scripts in Python, then you are advanced. What are you waiting for? Just purchase the course materials, progress through the labs, and take the course already! If you have not done that, do. Get an HTB subscription and progress through TJ Null's OSCP list while watching every IppSec video forever box you do, earn your ten bonus points by completing the exercises and labs in the OSCP material, and go through all your notes and make sure you understand every page; otherwise toss it or rewrite it. Seriously, if you are at this stage, you are either underrating your own skills or pumping up the OSCP higher than it is. HTB boxes are the exact same as the labs and while the OSCP certification is difficult, any topic on the test will and has to be covered in the training material. When you take the test and pass, your first thought will be, "Wait, that's all it was?".


No matter what stage of learning you are in, notes are key. You will never remember every command or even the steps you took for that HTB box you solved a week ago. When pressure strikes in the exam, which it will, you are going to panic and run to whatever way you have been studying. If that means your notes are only a few pages long, most copy and pasted, and extraordinarily little personal notes, then you are absolutely going to fail. If your notes are organized, searchable, written out in your own language and never copied and pasted besides links and commands, cover every topic you have ever learned and include write-ups of your HTB boxes then there is no way you will fail. The OSCP tests your preparation, so if you have not put in the work, you will fail.

## Tips

Stuck on a box? Hop in the OSCP discord you now have access to and use the search function to find the name or IP of your box. Odds are someone has already run into the same issue and a student mentor was able to give them a few helpful hints. If you really cannot find any tips on where you are stuck, odds are you are in the wrong spot or completely missing something. Still think you are on the right path but need a hint? Feel free to @ the student mentors and they will get back to you when they can.

When trying to access computers behind a network, instead of complex port forwarding with Chisel, take a look at Ligolo-ng. Ligolo-ng allows you to tunnel to a network like a VPN, giving you the ability to access those new machines with no added syntax to your commands.

Too many times I got stuck because I did not have a variety of tools. Stuck on something that should work? Look up a different tool that does the same thing and try that one as well.

The struggle is where you really learn. When you are banging your head against the desk hour after hour on the same part, you are really learning more than you could from any book. While it does not feel good in the moment, the triumph of solving an issue that felt impossible is the best feeling in the world. Cherish those moments where you feel like you cannot do it because every time you will triumph. 

## Now What?

While the OSCP is a staple in our industry, it is quite surprising the lack of depth required to pass the OSCP. While the labs and topics can go into quite some detail, the true test can feel almost underwhelming and bland. Remember, no certification can prepare you for an interview. You can choose to skim over your learning and HTB boxes and still pass the test, but when it comes time to sit down in an interview, those experiences are the exact ones you want to rely upon and show as an example. Otherwise, you are left stuttering about general networking topics, and you quickly realize all you have is a piece of paper with your name on it and none of the knowledge you really need.

As for what to do after the OSCP, I will have to update this when I gain more experience and work insight.

However, if you are still feeling unsure and want more resources, please check out the links below. I did not want to bloat this post with too much information. Rather, all the posts below expand on topics I touched above to give you the alumni tips for everything you are about to do. These are what I wish I knew before I started doing each of these topics.



