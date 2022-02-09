---
id: 294
title: 'courses.edx.org : grep'
date: '2014-09-24T08:03:24+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=294'
permalink: /2014/09/courses-edx-org-grep/
categories:
    - Linux
tags:
    - grep
    - linux
---

| **Command** | **Usage** |
|:-:|:-:|
| grep \[pattern\] &lt;filename&gt; | Search for a pattern in a file and print all matching lines |
| grep -v \[pattern\] &lt;filename&gt; | Print all lines that do **not** match the pattern |
| grep \[0-9\] &lt;filename&gt; | Print the lines that contain the numbers 0 through 9 |
| grep -C 3 \[pattern\] &lt;filename&gt; | Print context of lines (specified number of lines above and below the pattern) for matching the pattern. Here the number of lines is specified as 3. |