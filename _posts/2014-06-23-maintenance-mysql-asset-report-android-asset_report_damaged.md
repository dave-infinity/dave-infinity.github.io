---
id: 195
title: 'Maintenance MySQL &#8211; Asset Report Android: asset_report_damaged'
date: '2014-06-23T07:34:58+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=195'
permalink: /2014/06/maintenance-mysql-asset-report-android-asset_report_damaged/
categories:
    - Uncategorized
tags:
    - android
    - asset_report_damaged
    - maintenance
    - mysql
---

CREATE VIEW asset\_report\_damaged AS  
SELECT  
a.ar\_id,  
a.ar\_barcode,  
x.al\_description,  
x.al\_asset\_group,  
x.al\_priloc,  
x.al\_secloc,  
x.al\_terloc,  
a.ar\_scandt,  
a.ar\_itemstatus,  
a.ar\_actiontaken,  
a.ar\_actionleft,  
a.ar\_datedue,  
a.ar\_userid,  
a.ar\_ts  
FROM asset\_report\_last a  
LEFT JOIN asset\_list x  
ON a.ar\_barcode=x.al\_barcode  
WHERE a.ar\_itemstatus NOT LIKE “%1%”;