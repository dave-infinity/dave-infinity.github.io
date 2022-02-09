---
id: 615
title: 'WSUS Installation'
date: '2016-04-08T09:55:54+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=615'
permalink: /2016/04/wsus-installation/
categories:
    - Microsoft
tags:
    - deployment
    - powershell
    - wsus
---

Attempting to install WSUS on server 2012 and then reinstall it.

The initial install went fine:

1/ Prepare security on directories: \[Network Service\] needs RWX on \[%windir%\\Microsoft.NET\\Framework\\v4.0.30319\\Temporary ASP.NET Files\] and \[%windir%\\Temp\] and \[D:\\WSUS\] folders

2/ Either select \[WIndows Server Update Services\] role from the GUI or in an elevated Powershell:

```
Install-WindowsFeature -Name UpdateServices -IncludeManagementTools 
```

3/ Launch postinstallation tasks through the GUI or Powershell command below. NOTE: if this is a reinstall then be sure to delete the previous database \[SUSDB\] from \[C:\\Windows\\WID\\Data\]

```
 C:\Program Files\Update Services\Tools\wsusutil.exe postinstall CONTENT_DIR=D:\WSUS 
```