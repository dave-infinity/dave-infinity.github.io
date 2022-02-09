---
id: 666
title: 'MySQL Commands Maintenance v2'
date: '2016-07-20T08:59:57+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=666'
permalink: /2016/07/mysql-commands-maintenance-v2/
categories:
    - MySQL
tags:
    - archive
    - export
    - mysql
---

## Create an Archive table for unused assets

This SQL statement creates the archive table based on any primary locations that equal ’23 Banbury Road’ or ‘Acland’, it then pulls in the data from the other reference tables.

CREATE TABLE `\_archive\_asset\_log\_verbose` AS  
SELECT  
`x`.`autonum`,  
`x`.`barcode`,  
`asset\_list`.`description`,  
`asset\_list`.`assetgroup`,  
`locations`.`priloc` as `locpriloc`,  
`locations`.`secloc` as `locsecloc`,  
`locations`.`terloc` as `locterloc`,  
`x`.`datedue`,  
`x`.`user`,  
`users`.`employeename`,  
`x`.`pdaid`,  
`pda`.`human` as `pda#`,  
`pda`.`pdauid`,  
`x`.`timecreated`,  
`x`.`status`,  
`x`.`actiontaken`,  
`x`.`actionremaining`,  
`x`.`checkrqd`,  
`x`.`changedesc`,  
`x`.`changegroup`,  
`x`.`changeloc`,  
`changeloc`.`priloc` as `changepriloc`,  
`changeloc`.`secloc` as `changesecloc`,  
`changeloc`.`terloc` as `changeterloc`,  
`x`.`ts`

FROM (((((maintenancev2.asset\_log as x  
LEFT JOIN `users` on `x`.`user`=`users`.`autonum`)  
LEFT JOIN `pda` on `x`.`pdaid`=`pda`.`autonum`)  
LEFT JOIN `asset\_list` on `x`.`barcode`=`asset\_list`.`barcode`)  
LEFT JOIN `locations` on `asset\_list`.`loc`=`locations`.`autonum`)  
LEFT JOIN `locations` as `changeloc` on `x`.`changeloc`=`changeloc`.`autonum`)

where `x`.`barcode` in  
(select `barcode` from `asset\_list` where `loc` in  
(select `autonum` from `maintenancev2`.`locations`  
where ((`priloc`=’23 Banbury Road’) or `priloc`=’Acland’)  
)  
);