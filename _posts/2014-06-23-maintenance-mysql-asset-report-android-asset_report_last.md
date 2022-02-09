---
id: 193
title: 'Maintenance MySQL &#8211; Asset Report Android: asset_report_last'
date: '2014-06-23T07:34:25+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=193'
permalink: /2014/06/maintenance-mysql-asset-report-android-asset_report_last/
categories:
    - Uncategorized
tags:
    - android
    - asset_report_last
    - maintenance
    - mysql
---

1\. asset\_report\_last\_sub  
CREATE VIEW asset\_report\_last\_sub AS SELECT ar\_barcode, MAX(ar\_ts) ar\_ts FROM asset\_report GROUP BY ar\_barcode;

2\. asset\_report\_last  
CREATE VIEW asset\_report\_last AS  
SELECT t.ar\_id, t.ar\_barcode, t.ar\_datedue, t.ar\_itemstatus, t.ar\_actiontaken, t.ar\_actionleft, t.ar\_userid, t.ar\_ts, t.ar\_scandt  
FROM asset\_report t  
LEFT JOIN asset\_report\_last\_sub x  
ON x.ar\_barcode=t.ar\_barcode AND x.ar\_ts=t.ar\_ts  
WHERE x.ar\_ts=t.ar\_ts;