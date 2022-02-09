---
id: 679
title: 'Linux Learnings'
date: '2016-07-22T09:36:07+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=679'
permalink: /2016/07/linux-learnings/
categories:
    - Linux
tags:
    - bash
---

```
dave@mule:~$ arr=($(ipcs -p | awk -F ' *' '$3 ~ /^[0-9]+$/ {print $3}' ))
```

```
dave@mule:~$ for i in "${arr[@]}"; do :; ps aux | grep -v grep | grep -e $i; done
```

This code firstly creates an array of the 3rd column’s numerical values from the \[ ipcs-p \] command and then in the second command it iterates over the array and filters out the \[ps aux\] results using \[grep\] to display only entries matching the item in the array.

It’s not terribly efficient but I’m just starting out here… 🙂