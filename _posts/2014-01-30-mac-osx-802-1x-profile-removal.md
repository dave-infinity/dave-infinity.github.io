---
id: 124
title: 'Mac OSX 802.1x Profile Removal'
date: '2014-01-30T12:24:06+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=124'
permalink: /2014/01/mac-osx-802-1x-profile-removal/
categories:
    - 'MAC OSX'
tags:
    - 802.1x
    - eduroam
    - Mac
    - 'wireless profile'
---

```
sudo mv /Library/Preferences/SystemConfiguration/com.apple.network.eapolclient.configuration.plist /Library/Preferences/SystemConfiguration/com.apple.network.eapolclient.configuration.plist.good
```