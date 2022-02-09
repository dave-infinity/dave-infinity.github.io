---
id: 853
title: 'Ubuntu, Kernel 4.14+, VMWare Workstation 14'
date: '2018-02-23T08:19:21+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=853'
permalink: /2018/02/ubuntu-kernel-4-14-vmware-workstation-14/
categories:
    - Linux
tags:
    - '14'
    - kernel
    - network.monitor
    - ubuntu
    - virtual
    - vmware
    - workstation
---

I was unable to compile the ubuntu kernel patches for VMWare Workstation 14.0 for a couple of reasons on Ubuntu 16.04 with an updated kernel v4.14:

1\. Launching VMWare Workstation resulted in a GUI window complaining no GCC-7.2 was available, solved by the following commands (thanks to <https://askubuntu.com/questions/859256/how-to-install-gcc-7-or-clang-4-0>) :

```
sudo add-apt-repository ppa:jonathonf/gcc-7.1
sudo apt-get update
sudo apt-get install gcc-7 g++-7
 
```

2\. The next failure was with further kernel compiling modules with the vmmonitor service failing. This needed a patch on the install scripts to support the latest kernel, resolved by the following commands (thanks to <https://github.com/mkubecek/vmware-host-modules/commit/770c7ffe611520ac96490d235399554c64e87d9f> for the patch and <https://superuser.com/questions/1255099/vmware-workstation-not-enough-physical-memory-since-last-update/1255963> for guidance on applying it):

```

~$ sudo cd /tmp
~$  cp /usr/lib/vmware/modules/source/vmmon.tar .
~$  tar xf vmmon.tar
~$  rm vmmon.tar
~$  wget <a href="https://raw.githubusercontent.com/mkubecek/vmware-host-modules/fadedd9c8a4dd23f74da2b448572df95666dfe12/vmmon-only/linux/hostif.c" rel="nofollow noreferrer">https://raw.gi </a>
thubusercontent.com/mkubecek/vmware-host-modules/fadedd9c8a4dd23f74da2b448572df95666dfe12/vmmon-only/linux/hostif.c
~$  mv -f hostif.c vmmon-only/linux/hostif.c
~$  tar cf vmmon.tar vmmon-only
~$  rm -fr vmmon-only
~$  mv -f vmmon.tar /usr/lib/vmware/modules/source/vmmon.tar
~$  vmware-modconfig --console --install-all

```