---
id: 139
title: 'WAIK Disable UAC'
date: '2014-02-19T12:54:00+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=139'
permalink: /2014/02/waik-disable-uac/
categories:
    - Deployment
    - Microsoft
    - Windows
tags:
    - deployment
    - uac
    - WAIK
---

Addition to WAIK sysprep xml to disable UAC

[ http://social.technet.microsoft.com/Forums/en-US/dc625f8b-9a51-4dc0-a573-8cc23cee12f8/can-uac-be-disabled-via-unattendxml-for-server-2008-deployments?forum=mdt](http://social.technet.microsoft.com/Forums/en-US/dc625f8b-9a51-4dc0-a573-8cc23cee12f8/can-uac-be-disabled-via-unattendxml-for-server-2008-deployments?forum=mdt "http://social.technet.microsoft.com/Forums/en-US/dc625f8b-9a51-4dc0-a573-8cc23cee12f8/can-uac-be-disabled-via-unattendxml-for-server-2008-deployments?forum=mdt")

&lt;component name=”Microsoft-Windows-Deployment” processorArchitecture=”amd64″ publicKeyToken=”31bf3856ad364e35″ language=”neutral” versionScope=”nonSxS” xmlns:wcm=”http://schemas.microsoft.com/WMIConfig/2002/State” xmlns:xsi=”http://www.w3.org/2001/XMLSchema-instance”&gt;  
&lt;RunSynchronous&gt;  
&lt;RunSynchronousCommand wcm:action=”add”&gt;  
&lt;Order&gt;1&lt;/Order&gt;  
&lt;Path&gt;net user administrator /active:yes&lt;/Path&gt;  
&lt;/RunSynchronousCommand&gt;  
&lt;RunSynchronousCommand wcm:action=”add”&gt;  
&lt;Order&gt;2&lt;/Order&gt;  
&lt;Path&gt;cmd /c reg add HKLMSOFTWAREMicrosoftWindowsCurrentVersionPoliciesSystem /v EnableLUA /t REG\_DWORD /d 0 /f&lt;/Path&gt;  
&lt;Description&gt;Disable EnableLUA&lt;/Description&gt;  
&lt;/RunSynchronousCommand&gt;  
&lt;RunSynchronousCommand wcm:action=”add”&gt;  
&lt;Order&gt;3&lt;/Order&gt;  
&lt;Path&gt;cmd /c reg add HKLMSOFTWAREMicrosoftWindowsCurrentVersionPoliciesSystem /v ConsentPromptBehaviorAdmin /t REG\_DWORD /d 0 /f&lt;/Path&gt;  
&lt;Description&gt;ConsentPromptBehaviorAdmin&lt;/Description&gt;  
&lt;/RunSynchronousCommand&gt;  
&lt;/RunSynchronous&gt;  
&lt;/component&gt;

```
<span style="line-height: 1.714285714; color: #444444; font-family: 'Open Sans', Helvetica, Arial, sans-serif; font-size: 1rem;"> </span>
```