---
id: 218
title: 'Maintenance MySQL &#8211; Job Sheets Android: locations_unique'
date: '2014-06-23T07:58:19+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=218'
permalink: /2014/06/maintenance-mysql-job-sheets-android-locations_unique/
categories:
    - Uncategorized
tags:
    - android
    - locations_unique
    - maintenance
    - mysql
---

CREATE VIEW locations\_distinctpri AS  
SELECT DISTINCT l\_priloc from locations;