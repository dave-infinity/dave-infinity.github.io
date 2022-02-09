---
id: 1026
title: 'Dell Perc RAID CLI'
date: '2020-07-07T09:01:34+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1026'
permalink: /2020/07/dell-perc-raid-cli/
categories:
    - Linux
tags:
    - dell
    - perc
---

The following are a few commands using the Dell perccli64 tool which can be downloaded from Dell (<https://www.dell.com/support/home/en-uk/drivers/driversdetails?driverId=F48C2>)

```
<pre class="wp-block-code">```
/opt/MegaRAID/perccli/perccli64 /c0 show 
/opt/MegaRAID/perccli/perccli64 /c0 /e32 show
```
```