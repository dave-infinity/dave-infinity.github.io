---
id: 935
title: 'Powershell : Domain Binding &#038; Description'
date: '2019-07-31T08:00:30+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=935'
permalink: /2019/07/powershell-domain-binding-description/
categories:
    - Powershell
tags:
    - add-computer
    - bind
    - domain
    - powershell
    - set-adcomputer
---

To bind a machine to the domain, rename it and put it in the desired OU:

```
<pre class="wp-block-code">```
Add-Computer -DomainName $FQDN -NewName $COMPUTERNAME -Credential $DOMAINBINDACCOUNT -OUPath "OU=SOMEOU, DC=test, DC=com" -restart
```
```

To replace an AD Computer object’s Description field:

```
<pre class="wp-block-code">```
$description = "This is a test description"
$ADComputer = get-adcomputer <ENGS-XXXX> -properties Description
Set-ADComputer $ADComputer -Description "$($ADComputer.Description) $description"
```
```