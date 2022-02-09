---
id: 306
title: 'courses.edx.org: z Command Family'
date: '2014-10-17T07:34:26+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=306'
permalink: /2014/10/courses-edx-org-z-command-family/
categories:
    - Linux
tags:
    - compressed
    - linux
    - z
---

<span style="text-decoration: underline;"></span>

| **Command** | **Description** |
|:-:|:-:|
| $ zcat compressed-file.txt.gz | To view a compressed file |
| $ zless &lt;filename&gt;.gz   or   $ zmore &lt;filename&gt;.gz | To page through a compressed file |
| $ zgrep -i less test-file.txt.gz | To search inside a compressed file |
| $ zdiff filename1.txt.gz   filename2.txt.gz | To compare two compressed files |