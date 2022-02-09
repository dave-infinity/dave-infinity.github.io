---
id: 688
title: 'Linx Tablet Windows 8.1 to Windows 10 Upgrade'
date: '2016-07-28T10:31:04+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=688'
permalink: /2016/07/linx-tablet-windows-8-1-to-windows-10-upgrade/
categories:
    - Hardware
tags:
    - linx
    - tablet
    - upgrade
    - 'windows 10'
---

Backup Process, pre-upgrade

Use a powered USB hub to connect the Linx OTG, USB (8GB) Pen drive, Large USB drive, keyboard and mouse

1. Backup the images via “File History” &gt; “System Image” to the large disk within Win8.1
2. Install Macrium Reflect Free
3. Create Macrium rescue USB drive and then boot into it (power off then hold power+vol up to get to boot mgr) to test it works
4. Reboot to Win8.1
5. Create backup images of the partitions using Macrium to the large USB drive

Upgrading:

1. Download all Windows updates to obtain the free upgrade to Windows 7 option
2. Export all drivers to the large backup disk (in my case the e:\\ drive) using PowerShell  
    NOTE: I didn’t actually need these, it’s good to backup though! ```
    <pre class="php">Export-WindowsDriver –Online -Destination e:\export-drivers
    ```
3. Download the drivers from the linx site [http://www.linxtablet.co.uk/page.php?p=windows-10-command-centre—drivers&amp;sid=ad908ed3eafdbd149ed7c8018a56e3af ](http://www.linxtablet.co.uk/page.php?p=windows-10-command-centre---drivers&sid=ad908ed3eafdbd149ed7c8018a56e3af) (you will need an account to do so, which is free)  
    NOTE: I didn’t actually need these, it’s good to backup though!
4. Run Windows Updates to get the upgrade (24 hours left at time of writing this oops!). I would guess it’s possible to create a bootable installation USB from licensed media in the future and will re-visit this guide when I do that.
5. Let Windows manage the installation, I had to install an external Micro SD Card to house the downloaded data.

Thanks to the following posts (login maybe required):

<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">http://www.linxtablet.co.uk/viewtopic.php?f=35&amp;t=1281 </div></figure><figure class="wp-block-embed"><div class="wp-block-embed__wrapper">http://www.linxtablet.co.uk/viewtopic.php?f=11&amp;t=1190&amp;start=40 </div></figure>