---
id: 855
title: 'Powershell : Query for user&#8217;s last logon date'
date: '2018-02-23T14:35:39+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=855'
permalink: /2018/02/powershell-query-for-users-last-logon-date/
categories:
    - Microsoft
tags:
    - active
    - ad
    - directory
    - last
    - logon
    - powershell
    - query
---

I needed to work out some AD accounts’ last logon dates to make a further assessment, in powershell I found this was fairly simple:

To get a list of all user attributes available for query:

> $&gt; get-aduser -identity &lt;USERNAME\_HERE&gt; -Properties \*

To query for last logon date:

> $&gt; get-aduser -identity &lt;USERNAME\_HERE&gt; -Properties LastLogonDate