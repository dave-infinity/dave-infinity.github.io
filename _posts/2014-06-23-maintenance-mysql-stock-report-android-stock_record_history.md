---
id: 198
title: 'Maintenance MySQL &#8211; Stock Report Android: stock_record_history'
date: '2014-06-23T07:43:48+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=198'
permalink: /2014/06/maintenance-mysql-stock-report-android-stock_record_history/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - stock_record_history
---

CREATE VIEW stock\_record\_history AS  
SELECT DISTINCT  
y.sr\_id,  
y.sr\_scandt,  
y.sr\_barcode,  
x.il\_description,  
x.il\_priloc,  
x.il\_secloc,  
x.il\_terloc,  
x.il\_group,  
y.sr\_qty,  
y.sr\_changedesc,  
y.sr\_changegroup,  
y.sr\_changepri,  
y.sr\_changesec,  
y.sr\_changeter,  
y.sr\_userid,  
y.sr\_deviceid,  
y.sr\_ts  
FROM item\_list x, stock\_record y  
WHERE y.sr\_barcode=x.il\_barcode;