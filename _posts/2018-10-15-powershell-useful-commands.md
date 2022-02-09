---
id: 901
title: 'Powershell  : Useful Commands'
date: '2018-10-15T17:16:22+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=901'
permalink: /2018/10/powershell-useful-commands/
categories:
    - Powershell
    - Uncategorised
tags:
    - get-adgroupmember
    - get-aduser
    - powershell
---

Get members of a group:

```
get-adgroupmember -identity <GROUPNAME>
```

Get a list of user’s “PasswordLastSet” field has a date greater than 31/01/2000 along with their usernames and email addresses:

```
get-aduser -filter * -Properties PasswordLastSet | where {$_.passwordLastSet -ge [DateTime] "01/31/2000 00:01 AM"} | Select-Object Name, PasswordLastSet, SamAccountName, EmailAddress
```

Compare two CSV files for differences:

```
$refCSV = import-csv .\Source.csv 
$compCSV = import-csv .\Reference.csv 
compare-object -referenceobject $refCSV -DifferenceObject $compCSV | foreach { $_.InputObject}
```

Iterate over a text file of usernames (one per line) and query AD for some values, printing the useraccount’s containing OU in a easily readable form and output to results.csv:

```
$usersaffected = "c:\tmp\listofusernames.txt"
$output = foreach ($line in get-content $usersaffected) {get-aduser $line -Properties * | Select @{l='OU';e={$_.DistinguishedName.split(',')[1].split('=')[1]}},"whenCreated", "emailaddress", "passwordLastSet", "distinguishedName"}
$output | export-csv -path c:\tmp\results.csv
```