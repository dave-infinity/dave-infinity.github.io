---
id: 200
title: 'Maintenance MySQL &#8211; Stock Report Android: stock_record_count'
date: '2014-06-23T07:46:40+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=200'
permalink: /2014/06/maintenance-mysql-stock-report-android-stock_record_count/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - stock_record_count
---

1\. stock\_record\_count\_sublocal  
CREATE VIEW stock\_record\_count\_sublocal AS  
SELECT sr\_barcode barcode, SUM(sr\_qty) qtyused  
FROM stock\_record  
GROUP BY barcode;

2\. stock\_record\_count\_subunion  
CREATE VIEW stock\_record\_count\_subunion AS  
(SELECT barcode, qtyused FROM **jobsheet\_report\_total**)  
union all  
(SELECT barcode, qtyused FROM stock\_record\_count\_sublocal);

3\. stock\_record\_count  
CREATE VIEW stock\_record\_count AS  
SELECT  
item\_list.il\_barcode,  
item\_list.il\_description,  
item\_list.il\_group,  
item\_list.il\_priloc,  
item\_list.il\_secloc,  
item\_list.il\_terloc,  
SUM(stock\_record\_count\_subunion.qtyused\* -1) stock\_level  
FROM item\_list  
INNER JOIN stock\_record\_count\_subunion  
ON item\_list.il\_barcode=stock\_record\_count\_subunion.barcode  
GROUP BY item\_list.il\_barcode;