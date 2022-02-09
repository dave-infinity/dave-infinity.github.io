---
id: 144
title: 'Allow Users to bind machines to domains'
date: '2014-02-19T13:27:51+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=144'
permalink: /2014/02/allow-users-to-bind-machines-to-domains/
categories:
    - Server
    - Windows
tags:
    - 'active directory'
    - 'delegate control'
    - 'domain bind'
---

Use the delegate Control wizard inside AD against the top level domain listing (not OU). You can then select “Join Domain” as a security option for your chosen user(s)/group(s).

Be sure to check for the group policy too, “Default Domain Policy” &gt; Computer Configuration &gt; Windows Settings &gt; Security Settings &gt; Local Policies &gt; “Add Workstations to Domain”