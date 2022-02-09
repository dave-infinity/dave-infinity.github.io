---
id: 339
title: 'Outlook : Powershell : Clear Duplicate Contacts'
date: '2014-11-10T12:20:05+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=339'
permalink: /2014/11/outlook-powershell-clear-duplicate-contacts/
categories:
    - Microsoft
tags:
    - contacts
    - duplicate
    - Outlook
---

\#########################################################  
\# #  
\# Remove Duplicate Outlook Contacts by Jean Louw #  
\# Blog http://powershellneedfulthings.blogspot.com/ #  
\# #  
\#########################################################

$olSession = (New-Object -ComObject Outlook.Application).Session  
$olSession.Logon(‘Outlook’) #Outlook is the profile name  
$contactsFolder = 10  
$tempFolderName = ‘temp\_folder\_’ + (get-date -Format ddmmyyyhhmmss)  
$myContacts = $olSession.GetDefaultFolder($contactsFolder).Items  
$tempFolder = $olSession.GetDefaultFolder($contactsFolder).Folders.Add($tempFolderName)

Write-Host “..getting unique items”  
$uniqueContacts = $myContacts | Sort FullName -Unique

\#move contacts to temp contacts folder  
foreach ($Contact in $uniqueContacts) {  
$Contact.Move($tempFolder) | foreach-object {Write-Progress “Backup unique items to temp folder…” $\_.FullName; $\_.FullName} | Out-Null  
}

\#read default contacts again and dump to csv  
Write-Host “..export duplicates to csv”  
$duplicates = $olSession.GetDefaultFolder($contactsFolder).Items  
$duplicates | Export-Csv duplicates.csv

\#delete all contacts left in default contacts folder  
Foreach ($duplicate in $duplicates){  
$duplicate.Delete() | foreach-object {Write-Progress “Deleting duplicate…” $\_.FullName; $\_.FullName} | Out-Null