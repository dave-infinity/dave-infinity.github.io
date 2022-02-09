---
id: 884
title: 'Cancelling a Scheduled chkdsk (Check Disk)'
date: '2018-05-04T13:35:02+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=884'
permalink: /2018/05/cancelling-a-scheduled-chkdsk-check-disk/
categories:
    - Microsoft
tags:
    - cancel
    - check
    - chksk
    - disk
    - registry
---

1. Boot from the Windows 10 DVD / install media
2. \[SHIFT\]+\[F10\] to reveal a command prompt
3. REGEDT32 to open registry editor
4. Highlight HKLM &gt; File &gt; Load Hive
5. Navigate to the local system disk :\\Windows\\System32\\config and open \[SYSTEM\]
6. Navigate to **HKEY\_LOCAL\_MACHINE\\&lt;LOADED HIVE NAME&gt;\\CurrentControlSet\\Control\\Session Manager\\**  and edit the **BootExecute** MULTI-SZ value to read only: **autocheck autochk \***
7. Reboot
8. tadaa!