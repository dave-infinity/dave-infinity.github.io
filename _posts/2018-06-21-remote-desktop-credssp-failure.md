---
id: 897
title: 'Remote Desktop CredSSP Failure'
date: '2018-06-21T12:30:40+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=897'
permalink: /2018/06/remote-desktop-credssp-failure/
categories:
    - Microsoft
tags:
    - connection
    - credssp
    - desktop
    - fail
    - oracle
    - rdp
    - remote
---

Temporary reprieve for affected clients:

```
REG ADD HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System\CredSSP\Parameters\ /v AllowEncryptionOracle /t REG_DWORD /d 2
```

Revert via this command once all remote connections are patched:

```
REG ADD HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System\CredSSP\Parameters\ /v AllowEncryptionOracle /t REG_DWORD /d 1
```