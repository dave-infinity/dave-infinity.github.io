---
id: 343
title: 'Outlook : Recreate autocomplete stream data'
date: '2014-11-12T09:55:42+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=343'
permalink: /2014/11/outlook-recreate-autocomplete-stream-data/
categories:
    - Microsoft
tags:
    - autocomplete
    - nk2
    - Outlook
---

1. Import the FirstName, LastName and EmailAddress from all sent emails into individual contacts in the” Suggested Contacts” folder inside of the systems default Outlook profile via:

powershell script **“import\_sent\_contacts\_updated.ps1”**

2\. Export the “Suggested Contacts” folder from within the Outlook “Options &gt; Advanced &gt; Export” feature. Filterout the fields so only Firstname, Lastname and EmailAddress are exported to an excel file

3\. Delete the “Suggested Contacts” list from Outlook

4\. Filter out the duplicates via “Filter &gt; Advanced Filter &gt; No Duplicates” from the excel file

5\. Extract firstname from email address excel formula where C2 contains the email address:

=IF(ISNUMBER(SEARCH(“@”,LEFT(C2,FIND(“.”,C2)-1))), LEFT(LEFT(C2,FIND(“.”,C2)-1),FIND(“@”,LEFT(C2,FIND(“.”,C2)-1))-1), LEFT(C2,FIND(“.”,C2)-1))

Extract the lastname if format is first.last:

=IF(ISNUMBER(SEARCH(“.”,C3)), RIGHT(MID(C3,FIND(“.”,C3),FIND(“@”,C3)-FIND(“.”,C3)),LEN(MID(C3,FIND(“.”,C3),FIND(“@”,C3)-FIND(“.”,C3)))-1),C3)

6\. Create a CSV from the excel file that has 3 columns (Type, Name, Email Address) where:

Type is “SMTP” or “EX” where SMTP=external addresses and EX=Exchange addresses

Name is “Firstname, Lastname”

EmailAddress is the email address

7\. Close Outlook

8\. Launch NK2Editor and open the steamautocomplete……dat file

9\. Delete the contents

10\. Action &gt; Import from simple CSV &gt; Select the formatted CSV file we created

11\. Save