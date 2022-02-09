---
id: 899
title: 'Powershell : Find users based on specific property and location'
date: '2018-10-13T09:33:44+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=899'
permalink: /2018/10/powershell-find-users-based-on-specific-property-and-location/
categories:
    - Powershell
tags:
    - get-aduser
    - powershell
---

``

```
get-aduser -filter * -SearchBase "OU=XXX, OU=XXX, DC=XXX, DC=XXX, DC=XXX, DC=XXX" -Properties PasswordLastSet
```