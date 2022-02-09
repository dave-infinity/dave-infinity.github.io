---
id: 187
title: 'Maintenance MySQL &#8211; Asset Report Android: asset_report_change_request'
date: '2014-06-23T07:32:09+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=187'
permalink: /2014/06/maintenance-mysql-asset-report-android-asset_report_change_request/
categories:
    - Uncategorized
tags:
    - android
    - asset_report_change_request
    - maintenance
    - mysql
---

CREATE VIEW asset\_report\_change\_request AS  
SELECT x.ar\_id, x.ar\_barcode, y.il\_description, y.il\_group, y.il\_priloc, y.il\_secloc, y.il\_terloc, x.ar\_userid, x.ar\_scandt, y.il\_ts, x.ar\_ts FROM asset\_report x  
LEFT JOIN item\_list y ON x.ar\_barcode=y.il\_barcode  
WHERE ar\_checkrqd=”Yes”;