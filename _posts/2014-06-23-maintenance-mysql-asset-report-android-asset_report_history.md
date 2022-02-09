---
id: 189
title: 'Maintenance MySQL &#8211; Asset Report Android: asset_report_history'
date: '2014-06-23T07:32:47+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=189'
permalink: /2014/06/maintenance-mysql-asset-report-android-asset_report_history/
categories:
    - Uncategorized
tags:
    - android
    - asset_report_history
    - maintenance
    - mysql
---

CREATE VIEW asset\_report\_history AS  
SELECT DISTINCT y.ar\_scandt, y.ar\_datedue, y.ar\_id, y.ar\_barcode, x.al\_description, x.al\_priloc, x.al\_secloc, x.al\_terloc, x.al\_asset\_group, y.ar\_itemstatus, y.ar\_actiontaken, y.ar\_actionleft, y.ar\_userid, y.ar\_pdaid, y.ar\_ts, y.ar\_checkrqd, y.ar\_changedesc, y.ar\_changegroup, y.ar\_changepri, y.ar\_changesec, y.ar\_changeter FROM asset\_list x, asset\_report y WHERE y.ar\_barcode=x.al\_barcode;