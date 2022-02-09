---
id: 1008
title: 'verifying RPM files'
date: '2020-02-19T09:22:17+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1008'
permalink: /2020/02/verifying-rpm-files/
categories:
    - Linux
---

The following command will report back the signing key and other useful details for an rpm package:

```
<pre class="wp-block-code">```
rpm -qp1 <rpm package name>
```
```