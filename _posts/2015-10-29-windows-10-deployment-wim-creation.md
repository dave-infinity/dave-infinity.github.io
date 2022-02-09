---
id: 579
title: 'Windows 10 Deployment &#8211; Wim Creation'
date: '2015-10-29T09:39:17+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=579'
permalink: /2015/10/windows-10-deployment-wim-creation/
categories:
    - Microsoft
    - Windows
tags:
    - adk
    - deployment
    - dism
    - 'windows 10'
---

I was struggling to start with creating an ‘Unattend.xml’ through the Windows System Image Manager.

I downloaded and installed the Windows 10 deployment and Imaging Tools Environment through the Windows Assessment and Deployment Kit (ADK) for Windows 10 available from [https://msdn.microsoft.com/en-us/windows/hardware/dn913721(v=vs.8.5).aspx ](http://go.microsoft.com/fwlink/p/?LinkId=526740). However when attempting to load the ‘\\sources\\install.wim’ file from the Windows 10 Enterprise DVD I received the error:

```
09:28 : This application requires version 10.0.10240.16384 of the Windows ADK.
Install this version to correct the problem
09:29 :
09:29 : Error opening Windows image at D:\sources\install.wim.

09:29 :
09:29 : System.ComponentModel.Win32Exception (0x80004005): An attempt was made to load a program with an incorrect format
at Microsoft.ComponentStudio.ComponentPlatformInterface.WimFileHandle..ctor(String wimPath)
at Microsoft.ComponentStudio.ComponentPlatformInterface.WimInfo..ctor(String wimPath)
at Microsoft.ComponentStudio.ComponentPlatformInterface.Cpi.OpenWim(String wimPath)
at Microsoft.ComponentStudio.ImagePicker.GetImageInfoFromPath(String path)
at Microsoft.ComponentStudio.ImagePicker.ValidateImageFileOrFolder(String fileOrFolder)
```

After much googling around I did find a reference to the problem (although sadly I’ve now lost the source!), the issue is the compression level of the .wim on the DVD as (I believe) it was authored through the MediaCreationTool and so has undergone some increased compression.

The solution is to use DISM (provided as part of the ADK kit) to re-compress the ESD-wim file into a format that can be used by the Windows System Image Manager for creating the Unattend.xml answer files. To do this I issued the following command from the “Windows Imaging and Tools Environment” which was running in an Elevated Administrative fashion, where D:\\ was my DVD drive assignment:

```
dism.exe /Export-Image /SourceImageFile:D:\sources\install.wim /SourceIndex:1 /DestinationImageFile:C:\install.wim /Compress:max
```

I hope this is of help to others!

Dave