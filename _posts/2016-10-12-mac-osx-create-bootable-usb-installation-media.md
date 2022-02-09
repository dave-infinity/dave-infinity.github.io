---
id: 725
title: 'MAC OSX Create Bootable USB Installation Media'
date: '2016-10-12T09:26:38+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=725'
permalink: /2016/10/mac-osx-create-bootable-usb-installation-media/
categories:
    - 'MAC OSX'
tags:
    - installation
    - Mac
    - media
    - osx
    - usb
---

Here is the command to create a bootable installation USB for the latest OSX 10.12 Sierra, it’s the same as previous releases, at least as far back as Mavericks 10.9 with the only change being the name of the installation.app (“Install macOS Sierra.app” in this case) and the name of the USB volume I’m writing to (“SierraInstaller” in this case).

```
sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/SierraInstaller --applicationpath /Applications/Install\ macOS\ Sierra.app --nointeraction &&say Done
```

Credits: http://osxdaily.com/2016/06/15/make-macos-sierra-beta-usb-boot-drive/