---
id: 795
title: 'Tracerplus : Change Connect Project via Text'
date: '2017-05-19T09:57:34+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=795'
permalink: /2017/05/tracerplus-change-connect-project-via-text/
categories:
    - Software
tags:
    - connect
    - desktop
    - move
    - tracerplus
---

Tracerplus Connect software makes a hardcoded reference to the linked Tracerplus Desktop project. However if you need to relocate the directory of the Desktop project that will break the Connect references to the fields and cause the synchronization to fail.

If you move the Desktop project the following workflow may be best:

1. Stop the Connect Server service
2. Move the Desktop project (via export &gt; import)
3. locate the “.tce” file in the Connect project directory and replace all occurrences of the string : ```
    projectfile="C:\TracerplusDesktop\Project\DesktopProject.tpp">
    ```
    
    with the new directory, so if the new dir is “D:\\TP” it would become:
    
    ```
    projectfile="D:\TP\DesktopProject.tpp">
    ```