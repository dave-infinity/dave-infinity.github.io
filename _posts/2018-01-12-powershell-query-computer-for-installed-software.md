---
id: 819
title: 'Powershell : Query Computer for Installed Software'
date: '2018-01-12T15:19:19+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=819'
permalink: /2018/01/powershell-query-computer-for-installed-software/
categories:
    - Powershell
tags:
    - 'installed programs'
    - powershell
    - ps
    - win32
---

Onwards with the powershell quest, this code queries the remote computer named “PC1” for installed software and writes the results to a local file “C:\\PC1\_InstalledPrograms.csv”. The ouput is filtered for the “Displayname”,”Publisher”,”Version” and sorted by DisplayName.

Note: it does require SCCM’s Software Centre installed I think!

```
PS C:\Windows\system32> get-wmiobject -class win32reg_addremoveprograms -computername PC1 | select-object Displayname,Publisher,Version | export-csv -path "c:\PC1.csv"
```