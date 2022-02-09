---
id: 781
title: 'Microsoft WSUS Rebuild'
date: '2017-05-04T12:09:48+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=781'
permalink: /2017/05/microsoft-wsus-rebuild/
categories:
    - Microsoft
tags:
    - rebuild
    - server
    - services
    - update
    - wid
    - windows
    - wsus
---

To re-install WSUS with a clean database i.e. no previous configuration:

Run Windows Powershell as Administrator and use the following commands:

- Uninstall-WindowsFeature -Name UpdateServices,Windows-Internal-Database -Restart

- Post restart, delete EVERYTHING in the C:\\Windows\\WID\\ (for Win 2012 r2) folder.

- Then run the following command to re-install WSUS:  
    Install-WindowsFeature UpdateServices -Restart

This only works on PowerShell 3 or higher.

UPDATE  
I had to run the postinstallation tasks manually via Powershell using the WID db, if using SQL you need to add in sql\_instance=

C:\\Program Files\\Update Services\\Tools\\WsusUtil.exe content\_dir=”&lt;&lt;dir of update download location&gt;&gt;

creds: <https://serverfault.com/questions/449914/how-to-completely-wipe-wsus-and-start-again>