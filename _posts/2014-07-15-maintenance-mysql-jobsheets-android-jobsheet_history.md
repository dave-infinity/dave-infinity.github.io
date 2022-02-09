---
id: 237
title: 'Maintenance MySQL &#8211; JobSheets Android:  Jobsheet_History'
date: '2014-07-15T14:01:43+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=237'
permalink: /2014/07/maintenance-mysql-jobsheets-android-jobsheet_history/
categories:
    - MySQL
tags:
    - android
    - jobsheet_history
    - maintenance
    - mysql
---

CREATE VIEW jobsheet\_history AS  
SELECT x.jr\_id, x.jr\_jobid, x.jr\_userid, x.jr\_user\_assigned, x.jr\_pdaid, x.jr\_datedue, x.jr\_scandt, x.jr\_priloc, x.jr\_secloc, x.jr\_terloc, x.jr\_workrqd, x.jr\_workcomp, x.jr\_workleft, x.jr\_jobcomp, x.jr\_timetaken,  
x.jr\_pu1barcode, p1.il\_description pu1desc, x.jr\_pu1qty,  
x.jr\_pu2barcode, p2.il\_description pu2desc, x.jr\_pu2qty,  
x.jr\_pu3barcode, p3.il\_description pu3desc, x.jr\_pu3qty,  
x.jr\_pu4barcode, p4.il\_description pu4desc, x.jr\_pu4qty,  
x.jr\_pu5barcode, p5.il\_description pu5desc, x.jr\_pu5qty,  
x.jr\_pu6barcode, p6.il\_description pu6desc, x.jr\_pu6qty,  
x.jr\_pu7barcode, p7.il\_description pu7desc, x.jr\_pu7qty,  
x.jr\_pu8barcode, p8.il\_description pu8desc, x.jr\_pu8qty,  
x.jr\_pu9barcode, p9.il\_description pu9desc, x.jr\_pu9qty,  
x.jr\_pu10barcode, p10.il\_description pu10desc, x.jr\_pu10qty, x.jr\_ts  
FROM (((((((((jobsheet\_report x  
LEFT JOIN item\_list as p1 on x.jr\_pu1barcode=p1.il\_barcode)  
LEFT JOIN item\_list as p2 on x.jr\_pu2barcode=p2.il\_barcode)  
LEFT JOIN item\_list as p3 on x.jr\_pu3barcode=p3.il\_barcode)  
LEFT JOIN item\_list as p4 on x.jr\_pu4barcode=p4.il\_barcode)  
LEFT JOIN item\_list as p5 on x.jr\_pu5barcode=p5.il\_barcode)  
LEFT JOIN item\_list as p6 on x.jr\_pu6barcode=p6.il\_barcode)  
LEFT JOIN item\_list as p7 on x.jr\_pu7barcode=p7.il\_barcode)  
LEFT JOIN item\_list as p8 on x.jr\_pu8barcode=p8.il\_barcode)  
LEFT JOIN item\_list as p9 on x.jr\_pu9barcode=p9.il\_barcode)  
LEFT JOIN item\_list as p10 on x.jr\_pu10barcode=p10.il\_barcode;