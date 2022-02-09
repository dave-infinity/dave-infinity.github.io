---
id: 220
title: 'Maintenance MySQL &#8211; Timesheets Android: time_sheet_last'
date: '2014-06-23T07:59:42+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=220'
permalink: /2014/06/maintenance-mysql-timesheets-android-time_sheet_last/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - time_sheet_last
---

1\. time\_sheet\_last\_sub  
CREATE VIEW time\_sheet\_last\_sub AS  
SELECT DISTINCT MAX(ts\_id) ts\_id, ts\_userid, ts\_WE, MAX(ts\_scandt) ts\_last\_synch  
FROM time\_sheet GROUP BY ts\_userid, ts\_WE;

2\. time\_sheet\_last  
CREATE VIEW time\_sheet\_last AS  
SELECT time\_sheet.\* from time\_sheet, time\_sheet\_last\_sub  
WHERE time\_sheet.ts\_id=time\_sheet\_last\_sub.ts\_id  
ORDER BY time\_sheet.ts\_id DESC;