---
id: 754
title: 'Group Policy Management &#8211; Outlook 2016 Policy GUI Bug'
date: '2017-03-09T11:06:19+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=754'
permalink: /2017/03/group-policy-management-outlook-2016-policy-gui-bug/
categories:
    - 'Group Policy'
    - Microsoft
tags:
    - cached
    - exchange
    - gpo
    - 'group policy'
    - mode
    - 'office 2016'
    - 'outlook 2016'
    - synchronization
---

After a little puzzling with MS Outlook 2016 Synchronization settings GPO I thought I’d share this small bug in the GUI (at least for our environment 2k8r2 ADs):

If you’re editing Outlook 2016 cached exchange mode duration:

\\User Configuration\\Policies\\Administrative Templates\\Microsoft Outlook 2016\\Account Settings\\Exchange\\Cached Exchange Mode\\Cached Exchange Mode Sync Settings

Then switching the option to “All” and re-opening the policy in the GUI will display it reverting to “Three Days”, this is a bug!

My solution was simply changing the setting to “All” and not returning to the GUI control of the policy, if I then exited the policy and returned to the Group Policy Management GUI, inspecting the policy’s \[Settings\] I found the “All” setting was retained behind the scenes.