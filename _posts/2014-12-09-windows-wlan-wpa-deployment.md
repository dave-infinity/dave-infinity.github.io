---
id: 346
title: 'Windows: WLAN WPA Deployment'
date: '2014-12-09T13:09:53+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=346'
permalink: /2014/12/windows-wlan-wpa-deployment/
categories:
    - Uncategorized
    - Windows
tags:
    - deployment
    - wireless
    - wlan
    - wpa
---

to deploy a wlan profile along with WPA2 key (in plain text so be warned!):

1\. Create the profile first and then use:

```
Netsh Wlan Export Profile Name="<<PROFILE NAME>>" key=clear
```

this dumps an xml in the current working directort with the password in plain text.

2\. You can then run:

```
netsh wlan add profile filename="<<new xml file name>>" user=all
```

to reimport it on another machine

Other netsh WLAN commands:  
http://windows.microsoft.com/en-GB/windows-8/manage-wireless-network-profiles

| <div class="table-cell-content"><span class="para">Task</span></div> | <div class="table-cell-content"><span class="para">Instructions</span></div> |
|---|---|
| <div class="table-cell-content">Delete a profile  </div> | <div class="table-cell-content">At the command prompt, type:  <span class="userInput">netsh wlan delete profile name=”ProfileName”</span>  </div> |
| <div class="table-cell-content">Show all wireless profiles on the PC  </div> | <div class="table-cell-content">At the command prompt, type:  <span class="userInput">netsh wlan show profiles</span>  </div> |
| <div class="table-cell-content">Show a security key  </div> | <div class="table-cell-content">At the command prompt, type:  <span class="userInput">netsh wlan show profile name=“ProfileName” key=clear</span>  </div> |
| <div class="table-cell-content">Move a network up in the priority list  </div> | <div class="table-cell-content">Connecting to a new network and choosing <span class="ui">Connect automatically</span> will place it at the top of the list.  </div> |
| <div class="table-cell-content">Stop automatically connecting to a network within range  </div> | <div class="table-cell-content">Tap or click the network in the network list, then click<span class="ui">Disconnect</span>.  </div> |
| <div class="table-cell-content">Stop automatically connecting to a network that’s out of range  </div> | <div class="table-cell-content">At the command prompt, type:  <span class="userInput">netsh wlan set profileparameter name=”ProfileName” connectionmode=manual</span>  </div> |