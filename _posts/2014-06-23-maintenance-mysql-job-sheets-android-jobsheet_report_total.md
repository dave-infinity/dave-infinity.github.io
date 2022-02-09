---
id: 210
title: 'Maintenance MySQL &#8211; Job Sheets Android: jobsheet_report_total'
date: '2014-06-23T07:55:44+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=210'
permalink: /2014/06/maintenance-mysql-job-sheets-android-jobsheet_report_total/
categories:
    - Uncategorized
tags:
    - android
    - jobsheet_report_total
    - maintenance
    - mysql
---

1\. jobsheet\_report\_total\_sub  
CREATE VIEW jobsheet\_report\_total\_sub(jobid, barcode, qty) AS  
(SELECT jr\_jobid jobid, jr\_pu1barcode Barcode, jr\_pu1qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu1barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu2barcode Barcode, jr\_pu2qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu2barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu3barcode Barcode, jr\_pu3qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu3barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu4barcode Barcode, jr\_pu4qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu4barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu5barcode Barcode, jr\_pu5qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu5barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu6barcode Barcode, jr\_pu6qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu6barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu7barcode Barcode, jr\_pu7qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu7barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu8barcode Barcode, jr\_pu8qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu8barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu9barcode Barcode, jr\_pu9qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu9barcode “”)  
union all  
(SELECT jr\_jobid jobid, jr\_pu10barcode Barcode, jr\_pu10qty qty FROM jobsheet\_report\_last\_entry WHERE jobsheet\_report\_last\_entry.jr\_pu10barcode “”);

2\. jobsheet\_report\_total  
CREATE VIEW jobsheet\_report\_total AS  
SELECT barcode, SUM(qty) qtyused  
FROM jobsheet\_report\_total\_sub  
GROUP BY Barcode;