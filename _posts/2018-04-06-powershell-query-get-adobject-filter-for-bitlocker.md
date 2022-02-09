---
id: 871
title: 'Powershell Query &#8211; get-ADObject filter for Bitlocker'
date: '2018-04-06T11:46:48+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=871'
permalink: /2018/04/powershell-query-get-adobject-filter-for-bitlocker/
categories:
    - Microsoft
tags:
    - get-adobject
    - powershell
---

The following command returns all objects in the specified OU (replace XXX with your own values) which have Bitlocker recovery information and what the recovery key is.

```
Get-ADObject -Filter "objectClass -eq 'msFVE-RecoveryInformation'" -SearchBase "OU=XXX, OU=XXX, OU=XXX, DC=XXX, DC=XXX, DC=XXX, DC=XXX" -Properties msFVE-RecoveryPassword,whenCreated
```

I’m only really interested in the machine name for review so the following command both chops the Distinguished name field and returns just the second part and then chops that part removing the “CN=” section whilst also returning just that column name from the above query.

```
Get-ADObject -Filter "objectClass -eq 'msFVE-RecoveryInformation'" -SearchBase "OU=XXX, OU=XXX, OU=XXX, DC=XXX, DC=XXX, DC=XXX, DC=XXX" | Select @{l='ComputerName';e={$_.DistinguishedName.split(',')[1].split('=')[1]}}
```

The tricky part was the select statement, here’s a brief breakdown of what it’s doing.

@{} defines an array to be returned, which we’ll expect although it could end up being an array of 1 or 0 with no results.

“l” is shorthand for “label” which is the column header.  
“e” is shorthand for “expression”.  
“$\_.” indicates a single item in the pipeline, the results of Get-ADObject are then piped and this catches them one at a time.  
“DistinguishedName.split(‘,’)\[1\].split(‘=’)\[1\]” takes the value of the name DistinguishedName being piped and splits it first by “,”, selecting the second item in the array that forms “\[1\]” is second when counting from 0. It then splits that string again on the “=” sign, returning the second part (the actual computer name alone!).

Phew!

Learned a little more, powershell syntax understanding on the up!