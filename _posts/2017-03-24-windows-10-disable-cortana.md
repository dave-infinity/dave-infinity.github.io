---
id: 762
title: 'Windows 10 Disable Cortana'
date: '2017-03-24T10:06:33+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=762'
permalink: /2017/03/windows-10-disable-cortana/
categories:
    - Microsoft
tags:
    - cortana
    - 'disable cortana'
    - 'windows 10'
---

Either through GPO :

Computer Configuration &gt; Administrative Templates &gt; Windows Components &gt; Search

– **Allow Cortana = DISABLED**

Or via the registry directly (always backup first – http://www.davegernon.co.uk/techblog/export-windows-registry/)

HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows Search

Create a DWORD-32Bit Value named and value:

AllowCortana=0