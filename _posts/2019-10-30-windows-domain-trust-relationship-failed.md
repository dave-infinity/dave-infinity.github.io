---
id: 953
title: 'Windows Domain Trust Relationship Failed'
date: '2019-10-30T11:59:20+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=953'
permalink: /2019/10/windows-domain-trust-relationship-failed/
categories:
    - Powershell
tags:
    - computer
    - domain
    - failed
    - logon
    - machine
    - password
    - relationship
    - trust
    - windows
---

```
<pre class="wp-block-code">```
$creds = get-credential
Test-ComputerSecureChannel -Repair -credential $creds
```
```