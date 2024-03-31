---
title: "PNPT: Everything You Need and Did Not Want To Know"
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
  - Certifications
tags:
  - cyber security
  - penetration testing
  - pnpt
  - HTB
---

This post has three headings depending on what information you need. 

1. My Journey is a recount of everything I have done in life and up to to prepare for the PNPT.
2. The Down Low is everything you want to know about the exam: how it feels, what you need to be prepared for, and what to expect.
3. Now What? is my exanding on the PNPT and where and what it fails to teach you.


{% capture fig_img %}
![Foo]({{ "/assets/tcmsecurity-PNPT.jpg" | absolute_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>TCM Security Certification PNPT.</figcaption>
</figure>


## My Journey

My cybersecurity journey began when I went to college. I had no previous knowledge of penetration testing or even how networks operated. I did, however, have a natural curiosity for how things worked, and this led me to be increasingly intrigued by technology. Like some of you, I chose to go into cybersecurity because everybody around me was telling me what a growing field it is and how easy it would be to get a well-paying job. This led me to earn both an associate degree in computer networking and cybersecurity. The main highlight of my classes was the ability to be enrolled in the Cisco Networking Academy, or as I like to call it: "CCNA on crack". I worked in our lab building real life networks with routers and switches, which cemented a basic knowledge of networking which I did not possess before. I did not know it at the time, but the Cisco Networking Academy was the most valuable thing in my degree.

After graduating, I got an entry level job performing tech support for a library. I had the opportunity to work under the current Network Admin for the library and glean real life experience on network administration, VPNs, and local and cloud backups. Working as tech support firmly cemented all the knowledge I had learned in college and allowed me to acquire a high working level of networking. Two years passed by, and I knew I could not work tech support for the rest of my life, so I decided to pursue some sort of higher education. Not wanting to go back to college, I settled on earning the PNPT and then OSCP security certifications. Many hours of research, mainly Reddit threads, went into selecting this path.

## The Down Low

The PNPT in my opinion is the most bang for buck certification that currently exists on the penetration testing market. At just a few hundred bucks for both exam materials and two exam attempts, I could not imagine entering the penetration field any other way as a broke ex college student. With my degrees in networking and cybersecurity, I found the initial sections on networking too simple, but for someone who does not have that previous experience it would be perfect. The recurring theme of the PNPT is practical knowledge. It will not teach you an all-inclusive view of networking, penetration testing, and programming. It will, however, give you everything you need to get your wheels rolling. For many, we want information we can put into action, not information that we keep on the back burner for when or if it is ever used. While the course bundle does include quite a few courses, I found only Practical Ethical Hacking, Linux Escalation, and Windows Escalation to be necessary for the course. The other two courses, while containing valuable information, did not have any application for me on the exam. I found common sense and understanding of business technological practices to be the only things that I needed.

The one area the PNPT fails is in the application sector. The lack of a live lab setting, say the OSCP for example, hurts and the alternative of downloading and running the free mentioned labs does little. TCM Security is extremely honest about this, and it is probably how they can make the class so cheap and urge you to get a subscription to Hack The Box. I would recommend watching the solutions for every lab included in the course but using HTB as your main source of practice. For any beginner thinking they can watch the course and then go and pass the test are sorely mistaken. Although you get quite a few days to pass the test, what you really need is muscle memory knowledge. The only way to acquire this is by practicing these techniques on HTB. Specifically, for that, I would recommend following TJ Nulls HTB list for the OSCP as some HTB boxes do not entirely apply to the PNPT and OSCP.

For more details on how to practice Hack The Box I highly recommend my other post on How To Practice Hack The Box Right which goes into everything I wish someone had taught me when I first stumbled in HTB.

Since you have two exam attempts, I would recommend intentionally failing the first attempt. Practice the easiest HTB boxes first and follow my study tips in my other post for a handful of boxes and then take your first whack at it. Go in with the mindset that you do not possess enough knowledge, you just need to gauge the depth. From here go on a rampage devouring HTB boxes until nmap, crack map exec, burp suite, and other common tools feel like child’s play. While moving up TJ Null's list is great, make sure to complete or study all the Active Directory Boxes as that is primarily what this test is based on. Do your due diligence, study HTB like it’s your life, breathe the Linux console, and at the end of the day don't forget that this is based on a real penetration test. Vulnerabilities may not be vulnerabilities but just misconfigured access. Switch your brain from mass scanning for an out-of-date version to thinking about how Steve has all his passwords named after his cats that he has posted on Facebook. The mindset of what do users fail to do rather than leveraging a multistep complex exploit. Though, like anything, it might require a little bit of both.

## Now What?
While this is quickly changing, the other unfortunate area where the PNPT fails is industry recognition. In my career, I have only seen the PNPT listed on a single job posting. In the opposite light, the OSCP certification by OffSec has an extreme amount of recognition. For my path, this was the next step for me; I even studied both the PNPT and OSCP materials at the same time for a "boost" of knowledge. As you may guess, I have also written a blog post on my OSCP journey and would recommend reading it if that is the path you want to pursue.
