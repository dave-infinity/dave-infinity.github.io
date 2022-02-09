---
id: 945
title: 'Linux du folder sizes'
date: '2019-08-01T11:39:42+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=945'
permalink: /2019/08/linux-du-folder-sizes/
categories:
    - Linux
tags:
    - du
    - folder
---

List all folders in the /path/to/parent directory along with their size in (h)uman readable (m)egabytes

```
<pre class="wp-block-code">```
du -mh /path/to/parent --max-depth=1
```
```