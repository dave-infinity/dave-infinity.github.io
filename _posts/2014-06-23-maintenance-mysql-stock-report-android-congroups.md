---
id: 206
title: 'Maintenance MySQL &#8211; Stock Report Android: congroups'
date: '2014-06-23T07:48:39+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=206'
permalink: /2014/06/maintenance-mysql-stock-report-android-congroups/
categories:
    - Uncategorized
tags:
    - android
    - congroups
    - maintenance
    - mysql
---

CREATE VIEW congroups AS  
SELECT DISTINCT itemgroup  
FROM t\_conlist;