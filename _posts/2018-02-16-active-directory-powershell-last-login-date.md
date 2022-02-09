---
id: 835
title: 'Active Directory Powershell Last Login Date'
date: '2018-02-16T10:07:28+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=835'
permalink: /2018/02/active-directory-powershell-last-login-date/
categories:
    - Microsoft
tags:
    - ad
    - date
    - last
    - login
    - powershell
    - ps
---

``

```
PS C:\> get-adcomputer -Filter 'Name -like "$COMPNAME_HERE*"' -Properties lastlogondate | select name,lastlogondate
```