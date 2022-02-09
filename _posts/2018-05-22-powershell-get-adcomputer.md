---
id: 887
title: 'Powershell Get-ADComputer'
date: '2018-05-22T15:08:23+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=887'
permalink: /2018/05/powershell-get-adcomputer/
categories:
    - Microsoft
tags:
    - get-adcomputer
    - powershell
---

The following Powershell commmand uses the Get-ADComputer cmdlet to query AD and return a CSV with the headers “OU”,”Name” &amp; “OperatingSystem”.  
It was designed to return this information to marry up with GPO controlled policies against the OUs so I could plan servicing schedules.

Note the “-Properties \*” to ensure the OperatingSystem value is available and the “-NoTypeInformation” to drop the header row of the CSV file and leave the column headers as the first row.

```
Get-ADComputer -Filter * -property * -SearchBase "OU=XXX, DC=XXX, DC=XXX, DC=XXX, DC=XXX" | Select @{l='OU';e={$_.DistinguishedName.split(',')[1].split('=')[1]}},"Name", "OperatingSystem" | export-csv -Path C:\SomeDir\SomeFile.csv -NoTypeInformation
```