---
id: 224
title: 'Maintenance MySQL &#8211; Timesheets Android: time_sheet_we_next'
date: '2014-06-23T08:01:08+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=224'
permalink: /2014/06/maintenance-mysql-timesheets-android-time_sheet_we_next/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - time_sheet_we_next
---

CREATE VIEW time\_sheet\_we\_next AS  
SELECT x.tsw\_we from time\_sheet\_we x  
WHERE x.tsw\_we &gt;=DATE\_SUB(now(), INTERVAL 21 DAY)  
AND x.tsw\_we <date_add day="" interval=""></date_add>