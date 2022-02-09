---
id: 564
title: 'Create El Capitan 10.11 USB Installer Disk'
date: '2015-10-07T12:30:30+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=564'
permalink: /2015/10/create-el-capitan-10-11-usb-installer-disk/
categories:
    - 'MAC OSX'
    - Uncategorised
tags:
    - '10.11'
    - 'Installer USB'
    - osx
---

1. Download the installer from the App Store but do not install it, close the installer when it launches
2. Format an 8GB+ USB Drive in the GUID type and Journaled (not case sensitive) partition
3. run the command (where Untitled is the name of the partition you created in step 1): ```
    sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app --nointeraction
    ```
4. Sit back and relax, smoke a pipe while you wait maybe