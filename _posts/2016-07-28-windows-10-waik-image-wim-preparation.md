---
id: 647
title: 'Windows 10 WAIK Image (.wim) Preparation'
date: '2016-07-28T09:15:03+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=647'
permalink: /2016/07/windows-10-waik-image-wim-preparation/
categories:
    - Deployment
tags:
    - deployment
    - WAIK
    - 'windows 10'
    - winpe
---

## Aim of this guide

This guide will walk through the steps I’ve taken to create a deployable Windows 10 Enterprise .wim image which can then be used to deploy Windows 10 across our domain via our PXE environment.

## Prepare a machine with Windows 10

The first step is to create an Autounattend.xml file which will be copied to a USB Pen drive and attached to a target test machine, in this case a Dell 9020 along with the Windows 10 Enterprise DVD. The presence of this file in an attached USB Pen drive will cause the installation of Windows 10 to become automated and will force the machine into \[Audit Mode\], which is where we can begin stripping out the unwanted Windows 10 Apps before sysprep-ing and powering down the machine.

One thing to note is that this answer file formats the disk under the GPT scheme, NOT MBR. So if you have an MBR formatted drive you’ll need to first reformat it as GPT. This can be completed using the Windows 10 Installation DVD by pressing SHIFT+F10 when booting from the DVD to open a command prompt followed by:

```
diskpart
```

```
list disk
```

```
select disk 0 
```

(where disk 0 is your target deployment disk indicated from list disk)

```
clean
```

```
covert gpt
```

I’m assuming that you’ve installed the \[Deployment Tools\] and, optionally the \[Windows Preinstallation Environment\] from the Windows 10 Automated Deployment Toolkit \[https://technet.microsoft.com/en-us/itpro/windows/deploy/windows-deployment-scenarios-and-tools\] on your development machine, in my case this is our Windows Server.

Launch \[as Administrator\] the Windows System Image Manager

It will need a valid \[install.wim\] from the \[sources\] directory of a LTSB release of Windows 10.  
Create an answer file with the following components and settings:

**1 windowsPE:**

- **amd64\_Microsoft-Windows-Internationl-Core-WinPE\_neutral**  
    InputLocale= en-GB  
    SystemLocale= en-GB  
    UILanguage= en-US  
    UserLocale= en-GB  
    **-&gt; SetupUILanguage**  
    UILanguage= en-US  
    WillShowUI= OnError
- **amd64\_Microsoft\_Windows\_Setup\_neutral**  
    **-&gt;-&gt;DiskConfiguration** WillShowUI= OnError  
    **-&gt;-&gt;-&gt; Disk\[DiskID=”0″\]** Action= AddListItem  
    DiskID= 0  
    WillWipeDisk= True  
    **-&gt;-&gt;-&gt;-&gt; CreatePartitions**  
    **-&gt;-&gt;-&gt;-&gt;-&gt; CreatePartition\[Order=”1″\]** Action= AddListItem  
    Extend= False  
    Order= 1  
    Size= 500  
    Type= Primary  
    **-&gt;-&gt;-&gt;-&gt;-&gt; CreatePartition\[Order=”2″\]** Action= AddListItem  
    Extend= False  
    Order= 2  
    Size=  
    Type= Primary  
    **-&gt;-&gt;-&gt;-&gt; ModifyPartitions**  
    **-&gt;-&gt;-&gt;-&gt;-&gt; ModifyPartition\[Order=”1″\]** Action= AddListItem  
    Active= true  
    Extend= false  
    Format= NTFS  
    Label= System  
    Letter= S  
    Order= 1  
    PartitionID= 1  
    **-&gt;-&gt;-&gt;-&gt;-&gt; ModifyPartition\[Order=”2″\]** Action= AddListItem  
    Active= true  
    Extend= false  
    Format= NTFS  
    Label= Windows  
    Letter= C  
    Order= 2  
    PartitionID= 2  
    **-&gt;-&gt;ImageInstall**  
    **-&gt;-&gt;-&gt;OSImage** WillShowUI= OnError  
    **-&gt;-&gt;-&gt;-&gt; InstallTo** DiskID= 0  
    PartitionID= 2  
    **-&gt;-&gt;UserData** AcceptEula= true  
    **-&gt;-&gt;-&gt;ProductKey** WilLShowUI= never

**4 specialize:**

- **amd64\_Microsoft-Windows-Deployement\_neutral**  
    **-&gt; RunAsynchronous -&gt;-&gt; RunAsynchronousCommand\[order=”1″\]** Action= AddListItem  
    Order= 1  
    path= net user administrator /active:yes
- **amd64\_Microsoft-Windows-Security-SPP-UX\_neutral** SkipAutoActivation= true
- **amd64\_Microsoft-Windows-Shell-Setup\_neutral** ComputerName= Replaceme1  
    DisableAutoDaylightTimeSet= false  
    RegisteredOrganisation= &lt;&lt;YOUR COMPANY HERE&gt;&gt;  
    RegisteredOwner= &lt;&lt;YOUR DEPARTMENT HERE&gt;&gt;  
    ShowPowerButtonOnStartScreen= true  
    ShowWindowsLive= false  
    SignInMode= 1  
    TimeZone= GMT Standard Time  
    **-&gt; OEMInformation** HelpCustomized= false  
    SupportHours= &lt;&lt;YOUR WORKING HOURS HERE&gt;&gt;  
    SupportPhone= &lt;&lt;YOUR PHONE NUMBER HERE&gt;&gt;  
    SUPPORTURL= &lt;&lt;YOUR SUPPORT WEBSITE HERE&gt;&gt;

**7. oobeSystem:**

- **amd64\_Microsoft-Windows-Deployement\_neutral  
    -&gt; Reseal** Mode= Audit
- **amd64\_Microsoft-Windows-Shell-Setup\_neutral** ShowWindowsLive= false  
    SignInMode= 1  
    TimeZone= GMT Standard Time  
    **-&gt; AutoLogon** Enabled= true  
    LogonCount= 5  
    Username= Administrator  
    **-&gt; OOBE** HideEULAPage= true  
    HideLocalAccountScreen= true  
    HideOEMRegistrationScreen= true  
    HideOnlineAccountScreens= true  
    HideWirelessSetupInOOBE= true  
    NetworkLocation= Work  
    ProtectYourPC= 1  
    **-&gt; UserAccounts**  
    **-&gt;-&gt; AdministratorPassword** Value= &lt;&lt;YOUR PASSWORD HERE&gt;&gt;

Save the file and then copy it to a USB Pen drive and attach it to the target test machine along with the Windows 10 DVD, power on and boot from DVD then make a cuppa while the system installs.

Once the installation has completed you should be logged in as the Administrator in Maintenance mode with a Sysprep GUI window open on-screen.

Now you can begin configuring applications and programs that you want to be installed or removed for all systems.

## Remove Apps from the Windows 10 Audit Mode Machine

To remove apps from Windows 10 you can use PowerShell commands:

```
Uninstall Calendar and Mail: Get-AppxPackage *windowscommunicationsapps* | Remove-AppxPackage
```

```
Uninstall Get Office: Get-AppxPackage *officehub* | Remove-AppxPackage
```

```
Uninstall Get Skype: Get-AppxPackage *skypeapp* | Remove-AppxPackage
```

```
Uninstall Get Started: Get-AppxPackage *getstarted* | Remove-AppxPackage
```

```
Uninstall Groove Music: Get-AppxPackage *zunemusic* | Remove-AppxPackage
```

```
Uninstall Microsoft Solitaire Collection: Get-AppxPackage *solitairecollection* | Remove-AppxPackage
```

```
Uninstall Money: Get-AppxPackage *bingfinance* | Remove-AppxPackage
```

```
Uninstall Movies & TV: Get-AppxPackage *zunevideo* | Remove-AppxPackage
```

```
Uninstall News: Get-AppxPackage *bingnews* | Remove-AppxPackage
```

```
Uninstall OneNote: Get-AppxPackage *onenote* | Remove-AppxPackage
```

```
Uninstall People: Get-AppxPackage *people* | Remove-AppxPackage
```

```
Uninstall Phone Companion: Get-AppxPackage *windowsphone* | Remove-AppxPackage
```

```
Uninstall Photos: Get-AppxPackage *photos* | Remove-AppxPackage
```

```
Uninstall Store: Get-AppxPackage *windowsstore* | Remove-AppxPackage
```

```
Uninstall Sports: Get-AppxPackage *bingsports* | Remove-AppxPackage
```

```
Uninstall Weather: Get-AppxPackage *bingweather* | Remove-AppxPackage
```

```
Uninstall Xbox: Get-AppxPackage *xboxapp* | Remove-AppxPackage
```

## Remove / Install Any Other Applications &amp; Sysprep

Complete any other software installations or removals you require and then prepare an “unattend.xml” answer file which will be used to configure the system the image is deployed to.

TODO : Details of initial unattend.xml

Copy the “unattend.xml” file to:

```
C:\Windows\System32\Sysprep\unattend.xml
```

Then sysprep the target machine using the following command:

```
C:\windows\system32\Sysprep\sysprep.exe /generalize /oobe /shutdown /unattend:"C:\Windows\System32\Sysprep\unattend.xml"
```

## Image the target machine, capture that .wim!

The next stage is to image the now shutdown machine’s partitions into .wim files. I created a bootable .iso file using the Windows 10 Automated Deployment Toolkit and then copied in the DISM folder (which includes the imagex.exe utility) into the ISO.

Copied from <https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/winpe-create-a-boot-cd-dvd-iso-or-vhd> :

**Install the Windows ADK**

- Install the following features from the [Windows Assessment and Deployment Kit (ADK)](http://go.microsoft.com/fwlink/p/?LinkID=526803): 
    - **Deployment Tools**: includes the **Deployment and Imaging Tools Environment**.
    - **Windows Preinstallation Environment** : includes the files used to install Windows PE.

**Install Windows PE to a DVD, a CD, or an ISO file**

1. Click **Start**, and type **deployment**. Right-click **Deployment and Imaging Tools Environment** and then select **Run as administrator**.
2. Create a working copy of the Windows PE files. Specify either x86 or amd64: ```
    copype amd64 C:\WinPE_amd64
    
    ```
3. Create an ISO file containing the Windows PE files: ```
    MakeWinPEMedia /ISO C:\WinPE_amd64 C:\WinPE_amd64\WinPE_amd64.iso
    
    ```
4. To burn a DVD or CD: In Windows Explorer, right-click the ISO file, and select **Burn disc image** &gt; **Burn**, and follow the prompts.

You can either burn that ISO to a CD or use an ISO virtual drive such as the Zalman ZM-VE400 <http://www.zalman.com/contents/products/view.html?no=161> to boot from.

Attach another larger disk drive to the system, or map a network drive from within the Windows 10 PE (Live) environment you’ve booted into and then run the following commands to image the partitions:

1. Identify the volume letter assigned to the SYSTEM and WINDOWS partitions using the following commands: ```
    Diskpart
    ```
    
    ```
    list vol
    ```
    
    TODO\* : IMAGE OF list vol OUTPUT
2. 