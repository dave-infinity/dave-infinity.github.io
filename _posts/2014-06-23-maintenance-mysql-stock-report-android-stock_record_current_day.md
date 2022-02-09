---
id: 208
title: 'Maintenance MySQL &#8211; Stock Report Android: stock_record_current_day'
date: '2014-06-23T07:54:23+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=208'
permalink: /2014/06/maintenance-mysql-stock-report-android-stock_record_current_day/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - stock_record_current_day
---

CREATE VIEW stock\_record\_current\_day AS  
SELECT \* FROM stock\_record  
WHERE  
stock\_record.sr\_ts &gt;=DATE\_SUB(now(), INTERVAL 1 DAY);