---
id: 757
title: 'Windows Software Won&#8217;t Uninstall &#8211; Reboot Required Despite Rebooting'
date: '2017-03-21T11:42:43+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=757'
permalink: /2017/03/windows-software-wont-uninstall-reboot-required-despite-rebooting/
categories:
    - Microsoft
    - Software
tags:
    - 'pending file operation'
    - pendingfileoperation
    - reboot
    - required
    - uninstall
---

If this problem happens then it may be a result of failing pending changes to the Windows OS. These file changes are listed in a registry key:

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\

under DWORD:

PendingFileRenameOperation

I would suggest first renaming this DWORD value, with the prefix “OLD\_” or something similar and then attempting the un/install again.

If there were some unexpected results in renaming the file it is trivial to remove the prefix and restore the system but best practice would include an entire registry export prior to fiddling!

http://www.davegernon.co.uk/techblog/export-windows-registry/