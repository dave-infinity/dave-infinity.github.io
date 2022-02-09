---
id: 771
title: 'Intel USB 3.0 eXtensible Controller for Intel® 7 Series/C216 Chipset Family Windows 7 x64 BSOD'
date: '2017-04-13T10:08:43+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=771'
permalink: /2017/04/intel-usb-3-0-extensible-controller-for-intel-7-seriesc216-chipset-family-windows-7-x64-bsod/
categories:
    - Drivers
tags:
    - '0x0000007e'
    - '3.0'
    - bsod
    - usb
    - usb3
---

We have a number of Dell Optiplex 9010’s in use running Windows 7 Enterprise x64 which have Intel’s USB 3 chipset C216. However, the Dell cab file of drivers did not appear to contain a suitable driver for the systems via our deployment mechanism.

Once the machines were imaged and booting I attempted to install the latest USB3 driver from the Dell support pages (v1.0.8.251 ,A05) but the installation failed with a BSOD (Stop 0x0000007e), no matter how I tried to install the driver.

I then tried an older version (v1.0.6.245,A03) and that exhibited the same symptoms.

I then tried the oldest version available from Dell (v1.0.4.220,A01) and this worked without a BSOD! Note it’s the “Chipset\_Driver\_JPJJT\_WN32\_1.0.4.220\_A01.EXE” file.

Hope this helps others!