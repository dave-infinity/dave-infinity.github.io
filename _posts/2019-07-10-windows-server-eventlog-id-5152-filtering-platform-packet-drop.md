---
id: 928
title: 'Windows Server eventlog ID 5152 Filtering Platform Packet Drop'
date: '2019-07-10T13:04:38+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=928'
permalink: /2019/07/windows-server-eventlog-id-5152-filtering-platform-packet-drop/
categories:
    - Windows
tags:
    - '5152'
    - 'bad packet filtering'
    - event
    - eventlog
    - eventviewer
    - server
---

After some online searching around EVENT ID 5152 which had started littering my DC’s eventlogs following some additional audit enabling I discovered how to silence these logs from the SECURITY eventlog, leaving them in place for the FIREWALL log instead:

```
<pre class="wp-block-code">```

auditpol /set /subcategory:"Filtering Platform Packet Drop" /success:disable /failure:disable
auditpol /set /subcategory:"Filtering Platform Connection" /success:disable /failure:disable
```
```

The 5152 event:

Log Name: Security  
Source: Microsoft-Windows-Security-Auditing  
Date: XXXX  
Event ID: 5152  
Task Category: Filtering Platform Packet Drop  
Level: Information  
Keywords: Audit Failure  
User: N/A  
Computer: XXXX  
Description:  
The Windows Filtering Platform has blocked a packet.

Application Information:  
 Process ID: 0  
 Application Name: –

Network Information:  
 Direction: Inbound  
 Source Address: XXXX  
 Source Port: 54915  
 Destination Address: XXXX  
 Destination Port: 54915  
 Protocol: 17

Filter Information:  
 Filter Run-Time ID: 85817  
 Layer Name: Transport  
 Layer Run-Time ID: 13  
Event Xml:  
  
 5152 0 0 12809 0 0x8010000000000000 437620320 Security XXXX   
 0 – %%14592 XXX 54915 XXXX 54915 17 85817 %%14597 13