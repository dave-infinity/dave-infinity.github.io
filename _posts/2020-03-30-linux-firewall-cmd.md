---
id: 1015
title: 'Linux firewall-cmd'
date: '2020-03-30T10:17:15+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1015'
permalink: /2020/03/linux-firewall-cmd/
categories:
    - Linux
tags:
    - firewall
    - firewall-cmd
---

A few useful firewall-cmd syntax examples:

```
<pre class="wp-block-code">```
firewall-cmd --permanent --add-rich-rule 'rule family="ipv4" service name="https" source address="<<CIDR SUBNET HERE>>"  accept'
```
```