---
id: 959
title: 'Powershell DHCP Commands'
date: '2019-11-07T09:59:58+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=959'
permalink: /2019/11/powershell-dhcp-commands/
categories:
    - Uncategorised
---

Get-DhcpServerv4Reservation

 Get-DhcpServerv4Lease -ComputerName “&lt;&lt;FQDN OF DHCP SERVER&gt;&gt;” -ScopeId &lt;&lt;SUBNET SCOPE EG 192.6.0.0&gt;&gt; | export-csv  
 -notype -path c:\\tmp\\CurrentDHCPLeasesForScope.csv