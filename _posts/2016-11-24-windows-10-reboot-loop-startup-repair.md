---
id: 734
title: 'Windows 10 Reboot Loop : Startup Repair'
date: '2016-11-24T16:19:31+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=734'
permalink: /2016/11/windows-10-reboot-loop-startup-repair/
categories:
    - Microsoft
tags:
    - 'reboot loop'
    - 'windows 10'
---

I came across an HP unibody laptop which was caught in a Windows 10 reboot recovery startup loop. Unable to complete an SFC scan I discovered a DISM command which will trash any pending disk actions and in this case allowed the system to boot to the login prompt (after throwing away a number of Windows updates).

```
dism.exe /image:C:\ /cleanup-image /revertpendingactions
```

> [How to Fix SFC /SCANNOW There is a System Repair Pending](https://support.4it.com.au/article/how-to-fix-sfc-scannow-there-is-a-system-repair-pending/)

<iframe class="wp-embedded-content" data-secret="225162nAle" frameborder="0" height="327" marginheight="0" marginwidth="0" sandbox="allow-scripts" scrolling="no" security="restricted" src="https://support.4it.com.au/article/how-to-fix-sfc-scannow-there-is-a-system-repair-pending/embed/#?secret=225162nAle" style="position: absolute; clip: rect(1px, 1px, 1px, 1px);" title="“How to Fix SFC /SCANNOW There is a System Repair Pending” — IT Knowledgebase" width="580"></iframe>