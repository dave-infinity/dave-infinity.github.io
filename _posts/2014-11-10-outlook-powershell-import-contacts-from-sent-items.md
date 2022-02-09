---
id: 341
title: 'Outlook : Powershell : Import contacts from sent items'
date: '2014-11-10T12:20:48+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=341'
permalink: /2014/11/outlook-powershell-import-contacts-from-sent-items/
categories:
    - Microsoft
tags:
    - contacts
    - Outlook
    - 'Sent Items'
---

<div class="line number1 index0 alt2">`$outlook` `= ``new-object` `-com` `outlook.application`</div><div class="line number2 index1 alt1">`$olFolders` `= ``"Microsoft.Office.Interop.Outlook.OlDefaultFolders"` `-as` `[type]`</div><div class="line number3 index2 alt2">`$namespace` `= ``$outlook``.GetNameSpace(``"MAPI"``)`</div><div class="line number4 index3 alt1">`$sentItems` `= ``$namespace``.getDefaultFolder(``$olFolders``::olFolderSentMail)`</div><div class="line number5 index4 alt2">`$alreadyAddedEmails` `= @() ``#Empty Array`</div><div class="line number6 index5 alt1">`$counter` `= 0;`</div><div class="line number7 index6 alt2">`$totalItems` `= ``$sentItems``.items.count;`</div><div class="line number8 index7 alt1">`Write-Host` `"Scanning through"` `$totalItems` `"emails in SentItems"`</div><div class="line number9 index8 alt2">`$contacts` `= ``$outlook``.Session.GetDefaultFolder(``$olFolders``::olFolderSuggestedContacts)`</div><div class="line number10 index9 alt1">`##############################################################################################################`</div><div class="line number11 index10 alt2">`# FUNCTION - Adds Name/Email to SuggestedContacts - Unless it has already been added before (by this script).`</div><div class="line number12 index11 alt1">`##############################################################################################################`</div><div class="line number13 index12 alt2">`Function` `AddToSuggestedContactsIfNotAlreadyAdded (``$name``, ``$email``)`</div><div class="line number14 index13 alt1">`{    `</div><div class="line number15 index14 alt2">`    ``if``((``$name` `-eq` `"``") -or ($email -eq "") -or ($name -eq $null) -or ($email -eq $null)){`</div><div class="line number16 index15 alt1">`        ``return;`</div><div class="line number17 index16 alt2">`    ``}    `</div><div class="line number18 index17 alt1">`    ``if ($name -like '*@*') {`</div><div class="line number19 index18 alt2">`    ``$name = $null`</div><div class="line number20 index19 alt1">`    ``}`</div><div class="line number21 index20 alt2">`    ``else {`</div><div class="line number22 index21 alt1">`        ``$name = $name.Replace("``'``", "").Replace("""", "")`</div><div class="line number23 index22 alt2">`    ``}`</div><div class="line number24 index23 alt1">`    ``$contactAlreadyAdded = $false`</div><div class="line number25 index24 alt2">`    ``foreach ($elem in $global:alreadyAddedEmails) {`</div><div class="line number26 index25 alt1">`        ``if(($elem.ToLower() -eq $email.ToLower())){`</div><div class="line number27 index26 alt2">`            ``$contactAlreadyAdded = $true`</div><div class="line number28 index27 alt1">`        ``if ($name -eq $null) { $name = "``** No Display Name **``" }`</div><div class="line number29 index28 alt2">`            ``Write-Host  ($global:counter)"``/``"($totalItems)  "``SKIPPED ``" $name.PadRight(25,"` `") "``-``" $email`</div><div class="line number30 index29 alt1">`            ``return;`</div><div class="line number31 index30 alt2">`        ``}`</div><div class="line number32 index31 alt1">`    ``}`</div><div class="line number33 index32 alt2">`    ``if(!$contactAlreadyAdded )    {`</div><div class="line number34 index33 alt1">`        ``$newcontact = $contacts.Items.Add()`</div><div class="line number35 index34 alt2">`        ``$newcontact.FullName = $name`</div><div class="line number36 index35 alt1">`        ``$newcontact.Email1Address = $email`</div><div class="line number37 index36 alt2">`        ``$newcontact.Save()`</div><div class="line number38 index37 alt1">`        ``$global:alreadyAddedEmails += $email`</div><div class="line number39 index38 alt2">`    ``if ($name -eq $null) { $name = "``** No Display Name **``" }`</div><div class="line number40 index39 alt1">`        ``Write-Host ($global:counter)"``/``"($totalItems)  "``ADDED   ``" $name.PadRight(25,"` `") "``-" ``$email`</div><div class="line number41 index40 alt2">`    ``}`</div><div class="line number42 index41 alt1">`}`</div><div class="line number43 index42 alt2">`# Loop through all emails in SentItems`</div><div class="line number44 index43 alt1">`$sentItems``.Items | % { `</div><div class="line number45 index44 alt2">`    ``#Loop through each recipient`</div><div class="line number46 index45 alt1">`    ``$_``.Recipients | %{`</div><div class="line number47 index46 alt2">`        ``AddToSuggestedContactsIfNotAlreadyAdded ``$_``.Name ``$_``.Address`</div><div class="line number48 index47 alt1">`    ``}`</div><div class="line number49 index48 alt2">`    ``$global:counter` `= ``$global:counter` `+ 1`</div><div class="line number50 index49 alt1">`}`</div>