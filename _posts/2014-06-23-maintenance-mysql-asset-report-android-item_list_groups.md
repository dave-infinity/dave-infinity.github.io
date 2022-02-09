---
id: 191
title: 'Maintenance MySQL &#8211; Asset Report Android: item_list_groups'
date: '2014-06-23T07:33:22+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=191'
permalink: /2014/06/maintenance-mysql-asset-report-android-item_list_groups/
categories:
    - Uncategorized
tags:
    - android
    - item_list_groups
    - maintenance
    - mysql
---

CREATE VIEW item\_list\_groups AS  
SELECT DISTINCT il\_group  
FROM item\_list;