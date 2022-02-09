---
id: 595
title: 'Mac OSX Hard Disk Recovery'
date: '2016-01-08T16:03:34+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=595'
permalink: /2016/01/mac-osx-hard-disk-recovery/
categories:
    - Apple
tags:
    - 'data recovery'
    - 'disk utility'
    - hdutil
    - photorec
---

Couldn’t mount a disk image taken from a failing HDD.

1\. Attach the image file in osx:  
hdiutil attach -noverify -nomount /path/to/disk.dmg

2\. Download Photorec from http://www.cgsecurity.org/wiki/TestDisk\_Download, unpack and launch the binary file

3\. Select the attached disk, confirm it’s name through terminal:  
diskutil list

4\. Configure options in Photorec and leave it restoring what it can!