---
id: 222
title: 'Maintenance MySQL &#8211; Timesheets Android:  time_sheet_last_month'
date: '2014-06-23T08:00:19+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=222'
permalink: /2014/06/maintenance-mysql-timesheets-android-time_sheet_last_month/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - time_sheet_last_month
---

CREATE VIEW time\_sheet\_last\_month AS  
SELECT \* from time\_sheet\_last t  
WHERE t.ts\_WE &gt;= DATE\_ADD(LAST\_DAY(DATE\_SUB(NOW(), INTERVAL 2 MONTH)), INTERVAL 1 DAY);