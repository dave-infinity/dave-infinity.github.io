---
id: 369
title: 'tcpdump notes'
date: '2015-02-23T10:43:11+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=369'
permalink: /2015/02/tcpdump-notes/
categories:
    - Linux
    - Networking
tags:
    - dhcp
    - linux
    - networking
    - tcpdump
---

sudo tcpdump -i eth0 port 67 or port 68 -nev and “ether host &lt;&lt;MAC ADDRESS&gt;&gt;”

ether host &lt;mac address&gt;

verbose:

-vv

packet size for full details:

-s 1500

prevent name resolution:

-n