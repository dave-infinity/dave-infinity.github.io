---
id: 783
title: 'Windows Server 2012 .NET'
date: '2017-05-04T16:15:01+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=783'
permalink: /2017/05/windows-server-2012-net/
categories:
    - Windows
tags:
    - .net
    - '2012'
    - server
---

Dism /online /enable-feature /featurename:NetFX3 /featurename:NetFx3ServerFeatures /Source:X:\\sources\\sxs  
Note: X: is the drive letter of DVD drive on the computer, adjust it accordingly.