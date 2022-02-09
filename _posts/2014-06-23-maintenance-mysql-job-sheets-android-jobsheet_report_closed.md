---
id: 216
title: 'Maintenance MySQL &#8211; Job Sheets Android: jobsheet_report_closed'
date: '2014-06-23T07:57:40+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=216'
permalink: /2014/06/maintenance-mysql-job-sheets-android-jobsheet_report_closed/
categories:
    - Uncategorized
tags:
    - android
    - jobsheet_report_closed
    - maintenance
    - mysql
---

CREATE VIEW jobsheet\_report\_closed AS  
SELECT \* FROM jobsheet\_report\_last\_entry

WHERE jr\_jobcomp=-1;