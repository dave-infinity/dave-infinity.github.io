---
id: 620
title: 'HP Printer Not Printing MS Office or Text Documents'
date: '2016-04-18T13:00:02+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=620'
permalink: /2016/04/hp-printer-not-printing-ms-office-or-text-documents/
categories:
    - Printing
tags:
    - HP
    - pcounter
    - printer
    - 'waiting for printer'
---

The Issue:

Colleagues reported that some MS Word and Excel documents were not printing. Jobs are spooled to the printer but the message in the print queue just reads:

Waiting for printer to print(30)

and the number then counts down to 0 but nothing prints.

Client Details:  
Windows x64  
MS Office 2010 fully patched  
HP Laserjet 2055dn &gt; HP Universal Print Driver x64 v6.0.0 via Windows 2008 x64 Print Server

The problem existed on my own PC too, printing to an HP m401dne printer under the same driver and print server, also on Windows 7 x64 with the same MS Office deployment.

Tested:

1\. Alternate UPD versions from 5.5.0, 5.7.0, 6.0.0, 6.1.0, 6.2.0

2\. Reinstalled MS Office

3\. Adobe Reader 11.0.15 print jobs were fine

4\. Text documents from notepad++ didn’t print

5\. Test prints printed

6\. Notepad (windows) documents printed

7\. Switched the printer port on the printer to a direct TCP/IP port and NOT through the PCounter port and it worked!

Solution:

Following test #7 above I began inspecting the PCounter ports, when creating a new PCounter port the default value for \[Speed cache buffer size\] was \[64KB\] but on the “broken” printer shares it had been set to \[disabled\]. Changing this to \[64 KB\] resolved the problem.