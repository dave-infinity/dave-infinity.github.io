---
id: 148
title: 'Manage System restore and Shadow Copies from the command line'
date: '2014-02-19T14:46:07+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=148'
permalink: /2014/02/manage-system-restore-and-shadow-copies-from-the-command-line/
categories:
    - Deployment
    - Windows
tags:
    - 'system restore'
    - vss
    - 'windows administration'
---

thanks to [http://www.ghacks.net/2012/10/05/manage-system-restore-from-the-command-line/](http://www.ghacks.net/2012/10/05/manage-system-restore-from-the-command-line/ "http://www.ghacks.net/2012/10/05/manage-system-restore-from-the-command-line/")

- *vssadmin list shadows* – This command lists all existing shadow copies on the system
- *vssadmin delete shadows /for=c: /oldest* – This command deletes the oldest shadow copy on drive C
- *vssadmin delete shadows /for=d: /all* – This command deletes all existing shadow copies on drive D
- *vssadmin delete shadows /for=c: /shadow=ID* – Deletes the selected shadow copy. The IDs are listed when you use the list shadows command.
- *vssadmin resize shadowstorage /for=c: /maxsize=2GB* – Sets the shadow storage for drive C to 2 Gigabyte. May delete existing restore points starting with the oldest if space is not sufficient to store all System Restore points