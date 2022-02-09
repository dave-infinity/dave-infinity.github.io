---
id: 1065
title: smbclient
date: '2021-09-28T19:54:01+01:00'
author: oxcompdave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1065'
permalink: /2021/09/smbclient/
categories:
    - Powershell
tags:
    - powershell
---

The following command enabled me to send a file from a linux host to a Windows SMB share

```
<pre class="wp-block-code">```
smbclient "//<HOST / IP>/<SHARENAME>" -U $username -c "put /path/to/local/linux/file $targetfilename_on_windows_host"
```
```