---
id: 318
title: 'Macbook / pro /air: Disable / Enable keyboard'
date: '2014-10-17T12:30:11+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=318'
permalink: /2014/10/macbook-pro-air-disable-enable-keyboard/
categories:
    - Apple
tags:
    - apple
    - disable
    - keyboard
    - Mac
---

```
<pre class="alt2" dir="ltr">sudo kextunload /System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyboard.kext/
```

```
<pre class="alt2" dir="ltr">sudo kextload /System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyboard.kext/
```

props to http://forums.macrumors.com/showthread.php?t=433407