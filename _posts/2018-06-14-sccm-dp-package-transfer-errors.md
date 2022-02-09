---
id: 892
title: 'SCCM DP Package Transfer Errors'
date: '2018-06-14T08:53:38+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=892'
permalink: /2018/06/sccm-dp-package-transfer-errors/
categories:
    - Microsoft
tags:
    - distribution
    - failed
    - package
    - point
    - sccm
    - transfer
---

## The Problem

After a DNS change on one of our Distribution Points within SCCM 2012 R2 I decided to remove the old DP entry and recreate it. Removing the DP was easy enough, drop the roles and then delete the server from Administration &gt; Servers and Site System Roles then wait 24 hours for synchronisation to remove the content from the DP.

I then created a new DP in SCCM under the new DNS name and monitored the package transfer via Monitoring &gt; Distribution Point Group Status &gt; All Site Distribution Points. The results looked bad, every package was failing to transfer.

## The Investigation

I then reviewed the PkgXferMgr.log file at \\\\&lt;&lt;SCCM PRI SITE&gt;\\SMS\_ES1\\Logs\\ which contained the errors:

```
Failed to get object class $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
~ExecStaticMethod failed (80041002) SMS_DistributionPoint, AddFile $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
CSendFileAction::AddFile failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
Failed to add the file bcmnfcscr7-x64.cat in content 01C39B5C-4DA1-4A0E-A328-3FD2AC9F500F. Error 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
CSendFileAction::AddFileMetaData failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
CSendFileAction::SendFiles failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
CSendFileAction::SendContent failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
~ Sending failed. Failure count = 24, Restart time = 14/06/2018 06:56:25 GMT Daylight Time $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.828-60><thread=9112 (0x2398)>
Failed to get object class $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.812-60><thread=5008 (0x1390)>
~ExecStaticMethod failed (80041002) SMS_DistributionPoint, AddFile $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.859-60><thread=5008 (0x1390)>
CSendFileAction::AddFile failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.859-60><thread=5008 (0x1390)>
Failed to add the file dptf_cpu.cat in content 08D125AE-8841-4C08-90AA-0D6B091B5C39. Error 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.859-60><thread=5008 (0x1390)>
CSendFileAction::AddFileMetaData failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.859-60><thread=5008 (0x1390)>
CSendFileAction::SendFiles failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.859-60><thread=5008 (0x1390)>
CSendFileAction::SendContent failed; 0x80041002 $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.859-60><thread=5008 (0x1390)>
~ Sending failed. Failure count = 24, Restart time = 14/06/2018 06:56:25 GMT Daylight Time $$<SMS_PACKAGE_TRANSFER_MANAGER><06-14-2018 06:26:25.859-60><thread=5008 (0x1390)>
```

Inspecting the D:\\ drive on the DP suggested the packages were actually being copied, there was plenty of capacity free on the taregt disk D:\\ and it’s used storage was increasing through the synch process.

I did some searching online and came across a blog which described the error I received exactly:

<http://www.christopherkibble.com/sccm-2012-dp-errors-sendfiles-failed>

Following this blog restored my DP’s synchronisation functionality! What follows is a copy and paste job for reference.

## The Solution

On the affected distribution point:

1. Backup the registry
2. elevated command prompt: ```
    cd c:\windows\system32\wbem
    for %F in (*.dll) do regsvr32 /s %F
    mofcomp -check AuditRsop.mof
    ```
3. Review the output of the mofcomp command, if it looks like it’ll compile continue else address any issues: ```
    mofcomp -AuditRsop.mof
    ```
4. Locate the SMS\_DP$ share directory ```
    cd SMS_DP$\sms\bin
    for %F in (*.dll) do regsvr32 /s %F
    mofcomp -check smsdpprov.mof
    ```
5. Review the output of the mofcomp command, if it looks like it’ll compile continue else address any issues:  
    mofcomp smsdpprov.mof
6. Reboot the DP
7. Monitor the distribution status from the SCCM console (Monitoring &gt; Distribution Point Group Status &gt; All Site Distribution Points)