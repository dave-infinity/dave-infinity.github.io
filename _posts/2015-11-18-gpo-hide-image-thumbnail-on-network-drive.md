---
id: 585
title: 'GPO : Hide Image Thumbnail on Network Drive'
date: '2015-11-18T11:55:58+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=585'
permalink: /2015/11/gpo-hide-image-thumbnail-on-network-drive/
categories:
    - Microsoft
tags:
    - gpo
    - thumbnail
    - thumbnails
---

To turn off the thumbnail preview in Windows Explorer on network drives use the GPO:

```
"User Configuration\Policies\Administrative Templates\Windows Components\Windows Explorer\Turn off the caching of thumbnails in hidden thumbs.db files"
```

and

```
"User Configuration\Policies\Administrative Templates\Windows Components\Windows Explorer\Turn off the caching of thumbnails and only display icons on network folders"
```