---
id: 366
title: 'Windows 7 SSD Tuning'
date: '2015-02-18T09:37:23+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=366'
permalink: /2015/02/windows-7-ssd-tuning/
categories:
    - Hardware
    - Microsoft
    - Windows
tags:
    - 'solid state drive'
    - 'ssd tuning'
    - 'windows ssd'
---

Source: [http://www.computing.net/howtos/show/solid-state-drive-ssd-tweaks-for-windows-7/552.html](http://www.computing.net/howtos/show/solid-state-drive-ssd-tweaks-for-windows-7/552.html "http://www.computing.net/howtos/show/solid-state-drive-ssd-tweaks-for-windows-7/552.html")

1. SATA Controller AHCI Mode
2. Enable TRIM elevated cmd prompt: “fsutil behavior query DisableDeleteNotify”
3. Disable System Restore (optional, recommended as it interferes with TRIM)
4. Disbaled disk drive indexing
5. Disbale Defrag on disk
6. Disable Page File (optional, space saving only)
7. Disable Hibernation (optional, space saving only): elevated cmd prompt: “powercfg -h off”
8. Disable Prefetch &amp; Superfetch: \[HKEY\_LOCAL\_MACHINECurrentControlSetControlSessionManagerMemory ManagementPrefetchParameters\] &gt;&gt; EnablePrefetcher and EnableSuperfetch = 0
9. Disable Windows Write-Cache Buffer Flusing : Device Manager &gt; Disk Drive &gt; Policies &gt; UNTICK “Enable write caching on the device”
10. Disable Windows Search and Superfetch : services.msc &gt; Superfetch = Disabled &amp;&amp; Windows Search = Disabled
11. Disable ClearPageFileAtShutdown and LargeSystemCache : \[HKEY\_LOCAL\_MACHINECurrentControlSetControlSessionManagerMemory Management\] &gt; ClearPageFileAtShutdown &amp;&amp; LargeSystemCache = 0