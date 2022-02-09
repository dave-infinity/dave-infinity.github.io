---
id: 214
title: 'Maintenance MySQL &#8211; Job Sheets Android:  jobsheet_report_open'
date: '2014-06-23T07:57:12+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=214'
permalink: /2014/06/maintenance-mysql-job-sheets-android-jobsheet_report_open/
categories:
    - Uncategorized
tags:
    - android
    - jobsheet_report_open
    - maintenance
    - mysql
---

CREATE VIEW jobsheet\_report\_open AS  
SELECT \* FROM jobsheet\_report\_last\_entry  
WHERE jr\_jobcomp=0  
OR jr\_jobcomp IS NULL ;