---
id: 764
title: 'Sophos Cloud / Enterprise Client Forcible Removal'
date: '2017-03-24T15:53:39+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=764'
permalink: /2017/03/sophos-cloud-enterprise-client-forcible-removal/
categories:
    - Sophos
tags:
    - force
    - protection
    - reboot
    - remove
    - required
    - sophos
    - tamper
    - uninstall
---

https://community.sophos.com/products/sophos-cloud/f/sophos-central/75044/re-register-computer-issue—no-tamper-protection-password

Tried this and it worked for me:

PHASE1:

To recover a tamper protected system, you must disable Enhanced Tamper Protection.

Do the following:

Boot the system into Safe Mode.

Click Start &gt; Run and type regedit and then click OK.

Go to the following location in the registry editor:

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Sophos MCS Agent and set the REG\_DWORD Start to 0x00000004

Go to the following location in the registry editor:

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Sophos Endpoint Defense\\TamperProtection\\Config

Set the following DWORD values to 0: SAVEnabled and SEDEnabled

Reboot the system in normal mode.

Taken from Article 124377

PHASE 2

Then I went to uninstall and got an uninstall error so I created a batch file with the following:

net stop “Sophos Anti-Virus”  
net stop “Sophos AutoUpdate Service”  
:Sophos AutoUpdate  
MsiExec.exe /qn /X{7CD26A0C-9B59-4E84-B5EE-B386B2F7AA16} REBOOT=ReallySuppress  
MsiExec.exe /qn /X{BCF53039-A7FC-4C79-A3E3-437AE28FD918} REBOOT=ReallySuppress  
MsiExec.exe /qn /X{9D1B8594-5DD2-4CDC-A5BD-98E7E9D75520} REBOOT=ReallySuppress  
:Sophos Anti-Virus (Endpoint)  
MsiExec.exe /qn /X{8123193C-9000-4EEB-B28A-E74E779759FA} REBOOT=ReallySuppress  
MsiExec.exe /qn /X{36333618-1CE1-4EF2-8FFD-7F17394891CE} REBOOT=ReallySuppress  
:Sophos Anti-Virus (Server)  
MsiExec.exe /qn /X{72E30858-FC95-4C87-A697-670081EBF065} REBOOT=ReallySuppress  
:Sophos System Protection  
MsiExec.exe /qn /X{1093B57D-A613-47F3-90CF-0FD5C5DCFFE6} REBOOT=ReallySuppress  
:Sophos Network Threat Protection  
MsiExec.exe /qn /X{66967E5F-43E8-4402-87A4-04685EE5C2CB} REBOOT=ReallySuppress  
:Sophos Health  
MsiExec.exe /qn /X{A5CCEEF1-B6A7-4EB4-A826-267996A62A9E} REBOOT=ReallySuppress  
MsiExec.exe /qn /X{D5BC54B8-1DA1-44F4-AE6F-86E05CDB0B44} REBOOT=ReallySuppress  
:SDU (1.x)  
MsiExec.exe /qn /X{4627F5A1-E85A-4394-9DB3-875DF83AF6C2} REBOOT=ReallySuppress  
:Heartbeat  
MsiExec.exe /qn /X{DFFA9361-3625-4219-82C2-9EF011E433B1} REBOOT=ReallySuppress  
:Sophos Management Communications System  
MsiExec.exe /qn /X{A1DC5EF8-DD20-45E8-ABBD-F529A24D477B} REBOOT=ReallySuppress  
MsiExec.exe /qn /X{1FFD3F20-5D24-4C9A-B9F6-A207A53CF179} REBOOT=ReallySuppress  
MsiExec.exe /qn /X{D875F30C-B469-4998-9A08-FE145DD5DC1A} REBOOT=ReallySuppress  
MsiExec.exe /qn /X{2C14E1A2-C4EB-466E-8374-81286D723D3A} REBOOT=ReallySuppress

Run that

PHASE 3:

It was still showing up in the Control Panel/Uninstall Programs which prevented installation again. Run Microsoft’s fix it:

<https://support.microsoft.com/en-us/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed>

Choose Sophos and uninstall.