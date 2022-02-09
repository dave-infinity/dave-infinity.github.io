---
id: 778
title: 'Open Sense (PFSense Fork) Notes'
date: '2017-05-03T08:34:29+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=778'
permalink: /2017/05/open-sense-pfsense-fork-notes/
categories:
    - Networking
tags:
    - gnat
    - nat
    - open
    - opn
    - sense
    - vlan
---

NAT Configuration on OpenSense

interface &gt; other types &gt; vlan &gt; Add

interfaces &gt; assignments &gt; Add new interface &gt; assign name, ip address, mru etc

Firewall &gt; nat &gt; outbound &gt; clone existing rule and edit network address &amp;