---
id: 805
title: 'Subinacl.exe Microsoft Service Permissions'
date: '2017-07-11T16:19:42+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=805'
permalink: /2017/07/subinacl-exe-microsoft-service-permissions/
categories:
    - Microsoft
tags:
    - acl
    - ownership
    - services
    - subinacl
---

A nice little tool to manage service permissions on Windows name subinacl is available at <https://www.microsoft.com/en-gb/download/details.aspx?id=23510>

Default install directory is “C:\\Program Files (x86)\\Windows Resource Kits\\Tools”  
Usage example for the ‘spooler’ service and the user domain\\username:

```
subinacl /service spooler /grant=domain\username=top
```