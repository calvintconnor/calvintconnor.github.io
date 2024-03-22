---
title: "How to Practice Hack The Box Machines Right"
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
  - Penetration Testing
tags:
  - penetration testing
  - HTB
---




{% capture fig_img %}
![Foo]({{ "/assets/" | absolute_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption> </figcaption>
</figure>


## My Journey
Like many who may be reading this I first learned about Hack The Box when I started my journey to become a penetration tester. I scoured the internet for blog posts on the OSCP and other security certifications to try and get an alumni opinion of how best to break into the cybersecurity world. Over and over again I kept hearing the same phrase: Hack The Box. I struggled for many months perfecting the art of extracting the most information from HTB labs and writeups. That is exactly what I want to share with you today, everything that those countless blog posts still failed to mention or warn against. For context, this informatin is coming from the point of view of never having done any type of penetration testing before.

## The Down Low
The road to mastering the Hack The Box platform is not an easy one to follow. For starters, all boxes that will have (legal) writeups and tutorials will have been offlined and only available to VIP subscriptions. All free, and active, boxes cannot have writeups, hints, or tutorials of any kind as solving them earns you points towards your ranking. For someone starting out we need these tutorials and hence, also need the VIP subscription. Once you have acquired this, I suggest following TJ Null's OSCP HTB preperation list followed in order from hardest to easiest machines. If you are truly just starting out you will have no idea what flow, pattern, or tips and tricks you should be following. Your methodology will be in scrambles or non-existent - and I can only suggest one think to fix it.

## IppSec
IppSec may be the single greatest resource to you at the time of beginning. The primary thing he teaches you in his HTB walkthrough videos are how to really think like a penetration tester. He does not just move through the solution steps. Instead, he will follow his natural train of thought and follow rabbit holes to show you how an actual mind would eventually find the solution. For easy ranked HTB boxes he will even not look at the solution but use purely his narrated knowledge to solve the box in a timely manner. I cannot describe how many tips, tricks, ideas, best practices, commands, and methodology I have learned by simply absorbing IppSec videos. In the true beginning, you might even want to consider watching IppSec's tutorial and then attempting to emulate his steps and process. After a few of these however, the best approach is to start the box blind and refer to this resource if you get stuck. An important thing to remember as a beginner is that you do not know what you do not know. Contrary to the Offsec belief of trying harder, you may simply not be aware of an attack path or ability an application or port possesses. There were countless times I would spend hours on a box and finally look up my next hint only to exclaim, "Nobody ever told me it could do that!". There comes a point, however, where you need to rather research what you do not know. Some boxes expect you to have zero clue how an application works and the true test of the box is the enumeration and understanding you can gain to reveal a trivial exploit. This conveniantlly has a color-coded guide. In my experience, I have found when boxes start to stray into medium difficulty, check the user rating rather than the official rating, the best course of action is to struggle. Obviously, if you have spent all day stuck in the same spot it may be time to look up a hint for time's sake. But a challenge will show you exactly what you do not know, the wholes in your methodology, and what you should have taken notes on that you totally thought you would just remember the next time it popped. This is, however, not the best way I would look up hints when you just need a nudge forward.

## 0xdf
0xdf's blog posts about Hack The Box boxes have to be my favorite written tutorials. While IppSec is great at running through the entirity of a box, 0xdf is great at showing you the next commnand you should run. Often times I have found a tool or box has been updated and the exact path that IppSec took is now outdated. Instead of listening through the whole hour long video for a mention of another tool or idea, 0xdf will often record every viable tool and path for solving. As a beginner, I cannot state how valuable it was to see every single command you need to enter written out. Where other tutorials will simply say to create an smb share and transfer a file, every time 0xdf will write out every command that needs to be entered. This helps you see the practical side of penetration tester where others bounce over topics considered to basic - but we are beginners, it is what we need! Other times I have found myself knowing what to do, but only needing the next command or a tool name to get me chugging again. Watching an IppSec video will often give away too much information and spoil the box, but I have found scrolling down only as far as the next line that you need in 0xdf's tutorial posts is just enough to give you a real hint and still make you work for it. After all, the goal of all this in the first place is to actually learn something.

## Now What?
In practice, you really cannot go wrong with diving in and finding out later. It is all practice, but for some of us, time may be a huge factor. You may only have a couple of hours every day to study and we need to make sure you are getting the best experience out of this platform that you can. I went through the months of struggling through Hack The Box and put together this blog post so you can understand what you really need to know. Feel free to check out my other blog posts where I try and rip away the curtains and give you the "down low" information you are really looking for when you stumbled across this blog.
