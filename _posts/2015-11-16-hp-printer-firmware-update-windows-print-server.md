---
id: 583
title: 'HP Printer Firmware Update : Windows Print Server'
date: '2015-11-16T14:19:57+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=583'
permalink: /2015/11/hp-printer-firmware-update-windows-print-server/
categories:
    - Microsoft
tags:
    - firmware
    - printer
    - update
---

I was needing to update the firmware on an HP P3015 Laserjet printer and the “Firmware Update” utility on the web interface was failing.

The solution that I found was to simply copy the firmware update binary file to the printer via it’s UNC share name from the print server!

```
copy /b <firmware file> \\SERVER\PrinterShareName
```

This did the job perfectly!