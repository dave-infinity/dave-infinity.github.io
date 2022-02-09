---
id: 355
title: 'Technicolor TG582n Configuration'
date: '2015-01-11T11:11:37+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=355'
permalink: /2015/01/technicolor-tg582n-configuration/
categories:
    - Networking
tags:
    - 'home router'
    - technicolor
    - TG582
---

dhcp server lease list (lists the current DHCP clients)  
dhcp server lease delete clientid=xx:xx:xx:xx:xx:xx ( xx etc. is the MAC address of appropriate client from above list – deletes the current lease)  
dhcp server lease add clientid=xx:xx:xx:xx:xx:xx pool=LAN\_private addr=192.168.1.x leasetime=0 (adds required IP for appropriate client with infinite lease time)  
saveall