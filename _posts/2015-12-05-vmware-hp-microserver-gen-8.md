---
id: 588
title: 'VMWare HP Microserver Gen 8'
date: '2015-12-05T09:27:10+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=588'
permalink: /2015/12/vmware-hp-microserver-gen-8/
categories:
    - Virtualization
tags:
    - 'disk slow'
    - gen8
    - microserver
    - vmware
---

Had very slow disk performance on a RAID 1 array in ESXi on my new HP Gen 8 microserver and found hardware acceleration was disabled.

The answer appears to be rolling back the storage driver as per http://homeservershow.com/forums/index.php?/topic/9141-low-io-performance-with-esxi-60/page-3

esxcli software vib remove -n Hewlett-Packard:scsi-hpvsa  
esxcli software vib install –viburl=/vmfs/volumes/DATASTORE/scsi-hpvsa-5.5.0-88OEM.550.0.0.1331820.x86\_64.vib

Driver available from http://vibsdepot.hp.com/hpq/mar.30.2015/esxi-550-drv-vibs/hpvsa/

note:

First update all drivers via  
esxcli software vib update –depot=http://vibsdepot.hp.com/hpq/latest/index.xml –force  
esxcli software vib update –depot=http://vibsdepot.hp.com/hpq/latest/index-drv.xml –force