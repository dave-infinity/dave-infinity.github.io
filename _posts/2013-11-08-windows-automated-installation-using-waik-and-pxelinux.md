---
id: 7
title: 'Windows Automated Installation using WAIK and PXELinux'
date: '2013-11-08T11:40:41+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=7'
permalink: /2013/11/windows-automated-installation-using-waik-and-pxelinux/
categories:
    - Deployment
    - Microsoft
    - Windows
tags:
    - 'Automated Deployment'
    - 'Automated Install'
    - WAIK
    - 'Windows Installation'
---

This will be a rather lengthy initial post describing the process by which I’ve:

1. **Automated the installation of a Windows 7 PC using the WAIK scripted installation method**
2. **Captured an image (.wim file) of the Windows 7 installed PC**
3. **Injected drivers into the .wim file**
4. **Automated the offline injection of Windows updates into the .wim file every month**

PXE Windows PE covered in <http://www.monkeyandlamb.co.uk/itblog/pxelinux-windows-pe>

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**1. Automated the installation of a Windows 7 PC using the WAIK scripted installation method**

The first task was to automate the installation of a Windows 7 PC using an answer file, the WAIK tools enable the creation of such a file and a great guide can be found on technet:  
[http://technet.microsoft.com/en-us/library/dd349348(v=ws.10).aspx ](http://technet.microsoft.com/en-us/library/dd349348(v=ws.10).aspx "http://technet.microsoft.com/en-us/library/dd349348(v=ws.10).aspx")

I used the above article and some other sources online to create a “Autounattend.xml” file &lt;&lt;LINK TBC&gt;&gt; which when dropped onto a USB stick and attached to the target machine allowed automatic installation of Windows 7 Ent SP1 just by booting from the DVD.

This got me into “Audit” mode which is a pre-sysprep mode enabling me to make some basic additions to the machine before imaging.

I first installed the drivers that were missing and then rebooted (automatically returning to “Audit” mode!).

Next is ran the cmd “winsat prepop” which runs the Windows Assessment tool and allows Aero themes to run.

I then changed to the default aero theme **and installed the VMWare tools drivers so they don’t nerf physical installations!!!**

Finally I created the directory “C:WindowsSetupScripts” and copied my own personalised “SetupComplete.cmd” file which is just a batch file I created to clear the Autounattend.xml files from the system and then execute a registry key deletion by inserting a key that’s copied onto the target machines root C: drive by the PXELinux imaging process and finally to install our package deployment software (WPKG) if required and then to reboot.

If nothing else it’s definitely worth removing the Unattend.xml files used during the automated installation as these could contain delicate information:

```
del /Q /F c:windowssystem32sysprepunattend.xml
del /Q /F c:windowssystem32syspreppantherunattend.xml
del /Q /F c:windowspantherunattend.xml
```

The last step is to sysprep the machine specifying the Unattend.xml file you plan to use to deploy the image to your target machine(s).  
**Note:** this is very different to the “audit mode” Autounattend.xml crafted and used to create this initial base image.

The sysprep command I used (after copying Unattend.xml into “C:\\Windows\\System32\\Sysprep” dir was:

```
<strong>C:\windows\system32\sysprep\sysprep.exe /generalize /oobe /shutdown /unattend:"C:\windows\system32\sysprep\unattend.xml"</strong>
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**2. Capture an image (.wim file) of the Windows 7 installed PC**”

Booting from the Win 7 PXE image with imagex.exe included now allows imaging of the target machine.

Need to ensure you have suitable media to save disk .wim image to.

imagex is very easy to learn with /? for my project I needed both the Windows 7 SYSTEM partition and the PRIMARY OS partition. so two commands were required:

```

imagex.exe /capture C: Z:\disk-image-SYSTEM.wim /compress fast /verify "disk-image-SYSTEM"

imagex.exe /capture D: Z:\disk-image-PRIMARY.wim /compress fast /verify "disk-image-PRIMARY"
```

To continue to tidy up the image after injecting drivers and updates it needs to be re compressed occasionally:

```
imagex /export “G:\DeploymentShare\Operating Systems\ED\ED.wim” 1 c:\ED.wim /compress maximum

```