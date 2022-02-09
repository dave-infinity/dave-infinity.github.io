---
id: 204
title: 'Maintenance MySQL &#8211; Stock Report Android: stock_record_change_request'
date: '2014-06-23T07:48:06+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=204'
permalink: /2014/06/maintenance-mysql-stock-report-android-stock_record_change_request/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - stock_record_change_request
---

CREATE VIEW stock\_record\_change\_request AS  
SELECT  
x.sr\_id,  
x.sr\_barcode,  
x.sr\_changedesc,  
x.sr\_changegroup,  
x.sr\_changepri,  
x.sr\_changesec,  
 x.sr\_changeter,  
y.il\_description,  
y.il\_group,  
y.il\_priloc,  
y.il\_secloc,  
y.il\_terloc,  
x.sr\_checkrqd,  
x.sr\_userid,  
x.sr\_ts  
FROM stock\_record x  
LEFT JOIN item\_list y ON x.sr\_barcode=y.il\_barcode  
WHERE x.sr\_checkrqd=”Yes”  
ORDER BY x.sr\_barcode;