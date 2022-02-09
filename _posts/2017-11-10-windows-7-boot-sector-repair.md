---
id: 814
title: 'Windows 7 Boot Sector Repair'
date: '2017-11-10T14:57:27+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=814'
permalink: /2017/11/windows-7-boot-sector-repair/
categories:
    - Microsoft
tags:
    - bcdedit
    - boot
    - bootmgr
    - bootrec
    - loader
    - 'windows 7'
---

### The Scenario

I was working on a dual booted MBR style disk which had Windows 7 and Ubuntu installed. I was asked to remove the Ubuntu partition(s) and extend the Windows partition. The user had a backup of all data from the Ubuntu partition, not the Windows. The GRUB boot loader was in operation.

### The Solution

I began by backing up the disk.

I then booted into Windows and inspected the disk partitions via Disk Manager and (thankfully) found that Windows had been installed first, shrunk and then Ubuntu installed. This was apparent by seeing the order of partitions on the disk from left to right. I then deleted the 2 Ubuntu related partitions at the end of the disk (both were present after the Windows OS partition) and extended the Windows partition into the recovered space.

Then I rebooted into a Windows Recovery environment via a USB install I’d been supplied with and let Windows attempt a start-up repair, that failed and no valid Windows partitions were displayed, which might be normal if GRUB is controlling the bootloader but I’d have expected Windows PreInstalled Environment to detect the local partition.

I then opened a command prompt and ran the following commands:

```
bootrec /fixboot
```

-This ran successfully

```
bootrec /fixmbr
```

-This failed to complete, unable to find device or somesuch

```
bootrec /rebuildbcd
```

-This failed, it was unable to write to device

I spent a good hour attempting to manually rebuild the bootloader via bcdedit commands which eventually failed until I came across a thread suggesting the issue is booting from Windows 7 USB media.

I then dug out an old Windows 7 DVD and booted from that and voila, the above commands worked successfully. I did have to trash c:\\boot\\BCD via the commands:

```
attrib c:\boot\bcd -s -h
```

```
move c:\boot\bcd bcd.old
```

and then set the OS partition (no 100MB System partition on this disk) to active before running them successfully. I also then launched the Windows Startup Repair from within the DVD repair tools to correct any faults with active partitions etc. Following that the system booted.

Hope this helps someone, what should have take 15 mins ended up taking me 2 hours!