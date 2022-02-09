---
id: 202
title: 'Maintenance MySQL &#8211; Stock Report Android: stock_record_alert'
date: '2014-06-23T07:47:23+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=202'
permalink: /2014/06/maintenance-mysql-stock-report-android-stock_record_alert/
categories:
    - Uncategorized
tags:
    - android
    - maintenance
    - mysql
    - stock_record_alert
---

CREATE VIEW stock\_record\_alert AS  
SELECT il\_barcode, stock\_level  
FROM stock\_record\_count  
WHERE stock\_level