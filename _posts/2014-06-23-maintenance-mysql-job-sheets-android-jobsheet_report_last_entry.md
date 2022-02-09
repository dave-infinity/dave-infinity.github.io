---
id: 212
title: 'Maintenance MySQL &#8211; Job Sheets Android: jobsheet_report_last_entry'
date: '2014-06-23T07:56:41+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=212'
permalink: /2014/06/maintenance-mysql-job-sheets-android-jobsheet_report_last_entry/
categories:
    - Uncategorized
tags:
    - android
    - jobsheet_report_last_entry
    - maintenance
    - mysql
---

1\. jobsheet\_report\_last\_entry\_sub  
CREATE VIEW jobsheet\_report\_last\_entry\_sub AS  
SELECT MAX(jr\_id) id, jr\_jobid, MAX(jr\_scandt) scandt  
FROM jobsheet\_report  
GROUP BY jr\_jobid;

2\. jobsheet\_report\_last\_entry  
CREATE VIEW jobsheet\_report\_last\_entry AS  
SELECT x.\*  
FROM jobsheet\_report x, jobsheet\_report\_last\_entry\_sub y  
WHERE x.jr\_id=y.id;