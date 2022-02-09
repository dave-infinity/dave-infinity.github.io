---
id: 867
title: 'VMWare Workstation 14 Ubuntu'
date: '2018-03-08T12:19:20+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=867'
permalink: /2018/03/vmware-workstation-14-ubuntu/
categories:
    - Linux
    - Virtualization
tags:
    - allvmmemorylimit
    - memory
    - prefvmx
    - ram
    - ubuntu
    - vmware
    - workstation
---

I recently encountered a minor issue attempting to create additional VMs in VMWare Workstation 14 on Ubuntu. The error I received suggested there wasn’t enough memory free to power on an additional VM but the host has 32GB of RAM and I’d allocated 20GB across all VMs.

Inspecting the /etc/vmware/config file revealed the value:

```
prefvmx.allVMMemoryLimit = "12954"
```

Which is a hard upper limit for all VMs, adjusting it to the following with VMWare closed and then start VMWare resolved the problem:

```
prefvmx.allVMMemoryLimit = "20480"
```