---
id: 275
title: 'Networking in Linux'
date: '2014-09-18T08:30:26+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=275'
permalink: /2014/09/networking-in-linux/
categories:
    - Linux
tags:
    - linux
    - networking
---

| **Networking Tools** | **Description** |
|:-:|:-:|
| ethtool | Queries network interfaces and can also set various parameters such as the speed. |
| netstat | Displays all active connections and routing tables. Useful for monitoring performance and troubleshooting. |
| nmap | Scans open **ports** on a network. Important for security analysis |
| tcpdump | Dumps network traffic for analysis. |
| iptraf | Monitors network traffic in text mode. |

route -n (display routing)

sudo ethtool eth0

netstat -r

sudo nmap -sP &lt;network address&gt; (scan for open ports on network address ie: 192.168.0.0)