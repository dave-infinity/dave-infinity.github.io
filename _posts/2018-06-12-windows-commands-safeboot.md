---
id: 890
title: 'Windows Commands : Safeboot'
date: '2018-06-12T16:15:08+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=890'
permalink: /2018/06/windows-commands-safeboot/
categories:
    - Microsoft
tags:
    - bcdedit
    - mode
    - safe
---

Safe Mode:

```
<strong>bcdedit /set {default} safeboot minimal</strong>
```

Safe Mode with Networking:

```
<strong>bcdedit /set {default} safeboot network</strong>
```

Safe Mode with Command Prompt:

```
<strong>bcdedit /set {default} safeboot minimal
bcdedit /set {default} safebootalternateshell yes</strong>
```

To Remove either use msconfig to return to a normal boot or:

```
<strong>bcdedit /deletevalue {default} safeboot</strong>
```