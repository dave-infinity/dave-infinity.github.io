---
id: 378
title: 'Corrupted Hard Disk Recovery'
date: '2015-04-08T10:36:54+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=378'
permalink: /2015/04/corrupted-hard-disk-recovery/
categories:
    - 'MAC OSX'
tags:
    - 'data recovery'
    - dd
    - 'diskutil. osx'
    - 'hard disk'
---

Using “dd” inside of OSX I was able to copy the affected disk bit by bit to an image file and then convert that file to a readable format for OSX to mount:

1\. Get device ID of disk via

```
"diskutil list"
```

then created the image via:

```
dd bs=512 if=/dev/XXX of=/some_dir/foo.dmg conv=noerror,sync

```

2\. Next I converted the .dmg to an img for mounting via

```
hdiutil convert input.dmg -format UDTO -o output.img
```