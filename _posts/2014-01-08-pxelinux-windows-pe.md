---
id: 46
title: 'PXELinux Windows PE'
date: '2014-01-08T15:23:52+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=46'
permalink: /2014/01/pxelinux-windows-pe/
categories:
    - 'Pre Installed Environment'
    - Virtualization
    - Windows
---

The following batch file describes the creation of a Win7 PE boot environment and generates an ISO that is then bootable. For our needs we use PXELinux so note the echo in the batch file” echo Preparing peimagexfiles” below.

\[expand title=”Customized PE Creation batch file”\]

```

@echo off

set PEHOME=C:ITWAIK
set PEROOT=%PEHOME%_Mounts
set DRIVERSRC=%PEHOME%_SharedDrivers
set APPSRC=C:ITWAIK_SharedApplications

call "%PEHOME%_ProjectsWin7PEx86Environment2_create_winpe_imagepemount.bat"

rem dism seems to have a hissy fit with this in the command line so lets just do it first and use relative paths
rem (now fixed, but will leave as is)
cd /D "%PEHOME%"
cd ToolsPEToolsx86WinPE_FPs

echo Adding required components
dism /image:"%PEROOT%Mount" /add-package /packagepath:"%PEHOME%ToolsPEToolsx86WinPE_FPsWinPE-Scripting.cab"
dism /image:"%PEROOT%Mount" /add-package /packagepath:"%PEHOME%ToolsPEToolsx86WinPE_FPsWinPE-HTA.cab"
dism /image:"%PEROOT%Mount" /add-package /packagepath:"%PEHOME%ToolsPEToolsx86WinPE_FPswinpe-wmi.cab"
dism /image:"%PEROOT%Mount" /add-package /packagepath:"%PEHOME%ToolsPEToolsx86WinPE_FPswinpe-wmi.cab"

rem Show installed packages
dism /image:"%PEROOT%Mount" /get-packages

echo Adding drivers
Call "%PEHOME%_Sharedwinpe_inject_basic_network_drivers.bat"
echo Adding local apps and scripts

xcopy /s/e/i/y "%APPSRC%ghost" "%PEROOT%MountApplications"
xcopy /s/e/i/y "%APPSRC%imagex.exe" "%PEROOT%MountApplications"

copy /Y "%PEHOME%_ProjectsWin7PEx86Environment2_create_winpe_imageStartnet.cmd" "%PEROOT%MountWindowsSystem32startnet.cmd"

cd /D "%PEROOT%"

rem Remove 'press any key to boot' message
del isobootbootfix.bin

echo Preparing peimagexfiles
rd /s/q "%PEROOT%peimagex"
mkdir "%PEROOT%peimagex"

mkdir %PEROOT%peimagexFonts
copy %PEROOT%mountwindowsbootpxebootmgr.exe %PEROOT%peimagex
copy %PEROOT%mountwindowsbootpxepxeboot.n12 %PEROOT%peimagexpxeboot.0
copy %PEROOT%mountwindowsbootfontswgl4_boot.ttf %PEROOT%peimagexFonts
copy "%PEHOME%ToolsPEToolsx86bootboot.sdi" %PEROOT%peimagex

echo off > %PEROOT%peimagexempty

echo Creating the boot file
set BCDStore=%PEROOT%peimagexBCD
bcdedit -createstore %BCDStore%
bcdedit -store %BCDStore% -create {ramdiskoptions} /d "Ramdisk options"
bcdedit -store %BCDStore% -set {ramdiskoptions} ramdisksdidevice Boot
bcdedit -store %BCDStore% -set {ramdiskoptions} ramdisksdipath Bootboot.sdi
for /f "Tokens=3" %%i in ('bcdedit /store %BCDStore% /create /d "Windows 7 Install Image" /application osloader') do set GUID=%%i
bcdedit -store %BCDStore% -set %GUID% systemroot Windows
bcdedit -store %BCDStore% -set %GUID% detecthal Yes
bcdedit -store %BCDStore% -set %GUID% winpe Yes
bcdedit -store %BCDStore% -set %GUID% osdevice ramdisk=[boot]Bootboot.wim,{ramdiskoptions}
bcdedit -store %BCDStore% -set %GUID% device ramdisk=[boot]Bootboot.wim,{ramdiskoptions}
bcdedit -store %BCDStore% -create {bootmgr} /d "Windows 7 Boot Manager"
bcdedit -store %BCDStore% -set {bootmgr} timeout 30
bcdedit -store %BCDStore% -set {bootmgr} displayorder %GUID%

call "%PEHOME%_ProjectsWin7PEx86Environment2_create_winpe_imagepeunmount.bat"
copy %PEROOT%ISOsourcesboot.wim %PEROOT%peimagex

rem echo Creating CD ISO image
oscdimg -betfsboot.com iso pex86.iso

xcopy /s/e/i/y "%PEROOT%peimagex" "%PEHOME%_ProjectsWin7PEx86Environmentpeimagex"
xcopy /s/e/i/y "%PEROOT%pex86.iso" "%PEHOME%_ProjectsWin7PEx86Environment"

cd "%PEHOME%_ProjectsWin7PEx86Environmentpeimagex"

rmdir %PEROOT%
mkdir %PEROOT%
```

\[/expand\]