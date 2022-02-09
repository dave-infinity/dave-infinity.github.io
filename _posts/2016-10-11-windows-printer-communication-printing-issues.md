---
id: 722
title: 'Windows Printer Communication / Printing Issues'
date: '2016-10-11T13:12:49+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=722'
permalink: /2016/10/windows-printer-communication-printing-issues/
categories:
    - Microsoft
    - Printing
    - Windows
tags:
    - print
    - 'print queue'
    - printing
    - 'usb printer'
    - windows
---

This post is intended to cover a number of printing issues in Windows, I’ll add cases and solutions over time.

### Printer was installed and connected via USB but jobs showing in the queue and not printing / cancelling, preventing anything else from printing

1. <div>Click the [Start Orb]</div>
2. <div>Type: “services.msc” (without the quotation marks) into the search bar at the bottom of the [Start Menu]</div>
3. <div>A single result named “services” should appear, [Left Mouse Click] that link to open the Services Admin Console.</div>
4. <div>Locate the “Print Spooler” service in the list, a healthy print spooler service should look like the image below:</div><div>![Inline images 1](https://mail.google.com/mail/u/0/?ui=2&ik=1eac106c97&view=fimg&th=1578aa387ded9d0d&attid=0.1&disp=emb&realattid=ii_1578a932400a3bec&attbid=ANGjdJ9g3-fKgH1QCjZ7IDdXOKEdDe4JzhRkpsqAHnVuxQJIA22j2kp8fQs7hDCWS-P7MMqlDRgiqW_KbySw4BUbvu8C4tX0i10ynfmHloyYuKsYhDpJU0Te6LocQKI&sz=w1124-h40&ats=1476187857050&rm=1578aa387ded9d0d&zw&atsh=1)</div>
5. <div>If yours is in a “Stopped” state then continue to step 6, otherwise [Right Mouse Click] on the list entry for the service and [Left Mouse Click] “Stop”.</div>
6. <div>Now open Windows Explorer (My Computer for example), navigate to the following directly and delete all of the files you see in there: C:\Windows\System32\<wbr></wbr>spool\PRINTERS</div>
7. <div>Back to the “services admin console”, [Right Mouse Click] on the list entry for the service and [Left Mouse Click] “Start”.</div>
8. <div>If the service fails to start then note down the error message and let me know.</div>