---
id: 894
title: 'PowerShell : Editing File Properties'
date: '2018-06-21T11:41:22+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=894'
permalink: /2018/06/powershell-editing-file-properties/
categories:
    - Microsoft
tags:
    - editing
    - file
    - files
    - powershell
    - properties
---

Whilst writing a script which included a recycler section to ensure files older than 14 days were removed from a directory I needed a way to test the code. I then came across the set-itemproperty cmdlet which was just what I needed.

First i explored the cmdlet via:

```
get-help get-itemproperty
```

and

```
get-help get-itemproperty -examples
```

This then led me to run the commands

```
$folder = "C:\tmp\test"
```

```
get-itemproperty $folder | format-list -property *
PSPath : Microsoft.PowerShell.Core\FileSystem::C:\tmp\test
PSParentPath : Microsoft.PowerShell.Core\FileSystem::C:\tmp
PSChildName : test
PSDrive : C
PSProvider : Microsoft.PowerShell.Core\FileSystem
Mode : d-----
BaseName : test
Target : {}
LinkType :
Name : test
FullName : C:\tmp\test
Parent : tmp
Exists : True
Root : C:\
Extension :
CreationTime : 6/21/2018 11:30:13 AM
CreationTimeUtc : 6/21/2018 10:30:13 AM
LastAccessTime : 6/21/2018 11:30:13 AM
LastAccessTimeUtc : 6/21/2018 10:30:13 AM
LastWriteTime : 6/21/2018 11:30:13 AM
LastWriteTimeUtc : 6/21/2018 10:30:13 AM
Attributes : Directory
```

I wanted to set the creation and modified dates back in time to test my recyler one-liner, I acheieved this by first setting a variable to be a datetime object in the past (US date format so that’s the 31st January 2018):

```
$olddate = [datetime]"1/31/2018"
```

I then assigned this datetime value to the properties of the folder I wanted via the commands:

```
Set-ItemProperty $folder -Name CreationTime -Value $olddate
Set-ItemProperty $folder -Name LastWriteTime -Value $olddate
```

This worked a treat. I could then use this command to delete the folder and it’s contents if it was older than 14 days (credit to <https://www.thomasmaurer.ch/2010/12/powershell-delete-files-older-than/> for this one):

```
$Daysback = "-14"
$CurrentDate = Get-Date
$DatetoDelete = $CurrentDate.AddDays($Daysback)
Get-ChildItem C:\tmp | Where-Object { $_.LastWriteTime -lt $DatetoDelete } | Remove-Item -recurse -force
```