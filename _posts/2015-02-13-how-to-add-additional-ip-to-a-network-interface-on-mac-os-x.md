---
id: 360
title: 'HOW TO ADD ADDITIONAL IP TO A NETWORK INTERFACE ON MAC OS X'
date: '2015-02-13T13:47:42+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=360'
permalink: /2015/02/how-to-add-additional-ip-to-a-network-interface-on-mac-os-x/
categories:
    - 'MAC OSX'
    - Networking
tags:
    - 'additional ip'
    - Mac
    - 'mac networking'
    - osx
---

Source: [https://gerrydevstory.com/2012/08/20/how-to-create-virtual-network-interface-on-mac-os-x/](https://gerrydevstory.com/2012/08/20/how-to-create-virtual-network-interface-on-mac-os-x/ "https://gerrydevstory.com/2012/08/20/how-to-create-virtual-network-interface-on-mac-os-x/")

To add an additional IP to a network interface on OSX using the GUI simply “replicate service” on any interface via the cog in \[Network Settings\] and then assign the IP to the replicated interface manually.

source: [http://hints.macworld.com/article.php?story=20041223112819235](http://hints.macworld.com/article.php?story=20041223112819235 "http://hints.macworld.com/article.php?story=20041223112819235")

From the terminal:

sudo ifconfig en1 inet xxx.xxx.xxx.xxx netmask 255.255.255.0 alias

Where sudo = execute as root, en1 = the interface you want to add an alias to, xxx.xxx.xxx.xxx = ip you wan to add, 255.255.255.0 = desired netmask.