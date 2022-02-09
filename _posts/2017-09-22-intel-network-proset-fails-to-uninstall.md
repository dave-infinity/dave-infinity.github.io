---
id: 810
title: 'Intel Network ProSet Fails to Uninstall'
date: '2017-09-22T08:52:36+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=810'
permalink: /2017/09/intel-network-proset-fails-to-uninstall/
categories:
    - Microsoft
tags:
    - connections
    - driver
    - failed
    - intel
    - network
    - upgrade
    - 'windows 10'
---

I recently struggled to upgrade my Intel(R) Network Connections driver installation from v22.4.10 (unsupported in Windows 10 1703) due to a corrupted uninstaller.

Symptoms:

When attempting to install the latest supported driver (v22.6.6.0) the installer attempts to call any currently installed versions’ uninstaller and then fails with error 1703.

Resolution:

After much reading up I came across this post from days gone by referring the the last nuclear approach of MZIZAP <https://blogs.msdn.microsoft.com/ronalg/2012/06/07/troubleshooting-msi-uninstall-issuesintel-pro-network-connections-1713/> .  
That led me to search for modern alternatives which led me to the Windows 10 Helper utility <https://support.microsoft.com/en-gb/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed>

Launching that and first running it to repair the uninstaller and then again to forcibly remove it did the trick, I was then able to install the latest version.

I hope this helps someone else.