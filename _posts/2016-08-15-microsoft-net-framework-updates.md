---
id: 710
title: 'Microsoft .Net Framework Updates'
date: '2016-08-15T15:33:33+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=710'
permalink: /2016/08/microsoft-net-framework-updates/
categories:
    - Microsoft
tags:
    - .net
    - 4.6.1
    - deployment
    - dotnet
    - microsoft
---

Great article on command line switches for .Net Framework installation releases:

https://blogs.msdn.microsoft.com/astebner/2009/04/16/silent-install-repair-and-uninstall-command-lines-for-each-version-of-the-net-framework/

**.NET Framework 4 product family**

- [Download location](http://go.microsoft.com/fwlink/?LinkID=186916)
- [Deployment guide with silent install command lines](http://msdn.microsoft.com/library/ee942965(v=VS.100).aspx)

.NET Framework 4 Client Profile (32-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /q /norestart

.NET Framework 4 Client Profile (32-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /passive /norestart

.NET Framework 4 Client Profile (32-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /q /norestart

.NET Framework 4 Client Profile (32-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /passive /norestart

.NET Framework 4 Client Profile (64-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /q /norestart

.NET Framework 4 Client Profile (64-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /passive /norestart

.NET Framework 4 Client Profile (64-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /q /norestart

.NET Framework 4 Client Profile (64-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /passive /norestart

.NET Framework 4 Full (32-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /q /norestart

.NET Framework 4 Full (32-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /passive /norestart

.NET Framework 4 Full (32-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Extended\\setup.exe /uninstall /x86 /x64 /ia64 /parameterfolder Extended /q /norestart
> 
> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /q /norestart

.NET Framework 4 Full (32-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Extended\\setup.exe /uninstall /x86 /x64 /ia64 /parameterfolder Extended /passive /norestart
> 
> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /passive /norestart

.NET Framework 4 Full (64-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /q /norestart

.NET Framework 4 Full (64-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /repair /x86 /x64 /ia64 /parameterfolder Client /passive /norestart

.NET Framework 4 Full (64-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Extended\\setup.exe /uninstall /x86 /x64 /ia64 /parameterfolder Extended /q /norestart
> 
> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /q /norestart

.NET Framework 4 Full (64-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Extended\\setup.exe /uninstall /x86 /x64 /ia64 /parameterfolder Extended /passive /norestart
> 
> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\Client\\setup.exe /uninstall /x86 /x64 /parameterfolder Client /passive /norestart

**.NET Framework 4.5 product family**

- [.NET Framework 4.5 download location](http://www.microsoft.com/en-us/download/details.aspx?id=30653)
- [.NET Framework 4.5.1 download location](http://www.microsoft.com/en-us/download/details.aspx?id=40779)
- [.NET Framework 4.5.2 download location](http://www.microsoft.com/en-us/download/details.aspx?id=42642)
- [Deployment guide with silent install command lines](http://msdn.microsoft.com/en-us/library/ee942965(v=vs.110).aspx)

.NET Framework 4.5 (32-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\setup.exe /repair /x86 /x64 /ia64 /q /norestart

.NET Framework 4.5 (32-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\setup.exe /repair /x86 /x64 /ia64 /passive /norestart

.NET Framework 4.5 (32-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\setup.exe /uninstall /x86 /x64 /q /norestart

.NET Framework 4.5 (32-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\setup.exe /uninstall /x86 /x64 /passive /norestart

.NET Framework 4.5 (64-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\setup.exe /repair /x86 /x64 /ia64 /q /norestart

.NET Framework 4.5 (64-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\setup.exe /repair /x86 /x64 /ia64 /passive /norestart

.NET Framework 4.5 (64-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\setup.exe /uninstall /x86 /x64 /q /norestart

.NET Framework 4.5 (64-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\setup.exe /uninstall /x86 /x64 /passive /norestart

.NET Framework 4.5.1 (32-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /repair /x86 /x64 /ia64 /q /norestart

.NET Framework 4.5.1 (32-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /repair /x86 /x64 /ia64 /passive /norestart

.NET Framework 4.5.1 (32-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /uninstall /x86 /x64 /q /norestart

.NET Framework 4.5.1 (32-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /uninstall /x86 /x64 /passive /norestart

.NET Framework 4.5.1 (64-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /repair /x86 /x64 /ia64 /q /norestart

.NET Framework 4.5.1 (64-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /repair /x86 /x64 /ia64 /passive /norestart

.NET Framework 4.5.1 (64-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /uninstall /x86 /x64 /q /norestart

.NET Framework 4.5.1 (64-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.50938\\setup.exe /uninstall /x86 /x64 /passive /norestart

.NET Framework 4.5.2 (32-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /repair /x86 /x64 /ia64 /q /norestart

.NET Framework 4.5.2 (32-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /repair /x86 /x64 /ia64 /passive /norestart

.NET Framework 4.5.2 (32-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /uninstall /x86 /x64 /q /norestart

.NET Framework 4.5.2 (32-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /uninstall /x86 /x64 /passive /norestart

.NET Framework 4.5.2 (64-bit) – silent repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /repair /x86 /x64 /ia64 /q /norestart

.NET Framework 4.5.2 (64-bit) – unattended repair

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /repair /x86 /x64 /ia64 /passive /norestart

.NET Framework 4.5.2 (64-bit) – silent uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /uninstall /x86 /x64 /q /norestart

.NET Framework 4.5.2 (64-bit) – unattended uninstall

> %windir%\\Microsoft.NET\\Framework64\\v4.0.30319\\SetupCache\\v4.5.51209\\setup.exe /uninstall /x86 /x64 /passive /norestart