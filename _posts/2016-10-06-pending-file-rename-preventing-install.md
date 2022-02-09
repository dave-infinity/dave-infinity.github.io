---
id: 720
title: 'Pending File Rename Preventing Install'
date: '2016-10-06T13:30:26+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=720'
permalink: /2016/10/pending-file-rename-preventing-install/
categories:
    - Microsoft
tags:
    - 'pending file operation'
    - pendingfileoperation
    - registry
---

I had to install some Dell software but kept receiving the message “Unable to complete the installation due to pending file rename operation” on Windows 10 Enterprise.  
Renaming the registry key HKLM\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\PendingFileRenameOperations to HKLM\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\PendingFileRenameOperationsOLD allowed me to complete the installation.