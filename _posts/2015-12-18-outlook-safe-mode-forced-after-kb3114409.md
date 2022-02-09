---
id: 592
title: 'Outlook Safe Mode Forced after KB3114409'
date: '2015-12-18T08:53:46+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=592'
permalink: /2015/12/outlook-safe-mode-forced-after-kb3114409/
categories:
    - Microsoft
tags:
    - KB3114409
    - Outlook
    - 'safe mode'
---

This update, released 8th December 2015 caused safe mode to be forced for Outlook 2010.

No WSUS server so manual uninstall of the update can be achieved (at least on Windows 7 x64 Enterprise) via:

msiexec.exe /package {90140000-0011-0000-0000-0000000FF1CE} /uninstall {14CDCBF7-3CCC-42E2-A5BB-2D4926E16FAA} /norestart

ALWAYS check regedit for the {90140000-0011-0000-0000-0000000FF1CE} key first and examine the sub-key for KB3114409 to ensure this GUID is accurate!