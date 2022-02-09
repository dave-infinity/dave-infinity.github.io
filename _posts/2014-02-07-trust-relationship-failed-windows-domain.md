---
id: 134
title: 'trust relationship failed, windows domain'
date: '2014-02-07T13:01:04+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=134'
permalink: /2014/02/trust-relationship-failed-windows-domain/
categories:
    - Microsoft
tags:
    - ad
    - domain
    - trust
    - windows
---

```
HKLM\System\CurrentControlSet\services\Netlogon\Parameters
```

Change the value:

```
DisablePasswordChange=1
```

### 2016-07-21 UPDATE:

Discovered this thread which mentions using PowerShell to reset the machine password, if you haven’t completed the registry change:

Open PowerShell as administrator. Run this command sequence:

```
$credential = Get-Credential
```

(enter domain admin account when prompted)

```
Reset-ComputerMachinePassword -Server <<YOUR DC NAME HERE>>
```

Thanks to: [https://community.spiceworks.com/how\_to/108912-fix-the-trust-relationship-between-this-workstation-and-the-primary-domain-failed](https://community.spiceworks.com/how_to/108912-fix-the-trust-relationship-between-this-workstation-and-the-primary-domain-failed)