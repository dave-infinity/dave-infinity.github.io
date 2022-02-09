---
id: 384
title: 'monitor for dhcp offers on network'
date: '2015-04-23T08:51:35+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=384'
permalink: /2015/04/monitor-for-dhcp-offers-on-network/
categories:
    - Linux
    - Networking
tags:
    - dhcp
    - monitor
    - network
    - tshark
---

```
sudo ifconfig ethX promisc
tshark -i ethX -n port 68 -R 'bootp.type == 2'
```

Thanks to [http://blog.siufatfat.net/2013/08/25/locating-rogue-dhcp-on-linux/](http://blog.siufatfat.net/2013/08/25/locating-rogue-dhcp-on-linux/ "http://blog.siufatfat.net/2013/08/25/locating-rogue-dhcp-on-linux/")