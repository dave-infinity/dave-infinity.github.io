---
id: 966
title: 'Batch : Service Status &#038; Recovery'
date: '2019-11-18T08:52:32+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=966'
permalink: /2019/11/batch-service-status-recovery/
categories:
    - Microsoft
tags:
    - bat
    - batch
    - script
---

```
<pre class="wp-block-code">```
@echo off
 
REM Change the "servicename" value to match your desired service below
REM Change the "logfilename" value to your own logfile
REM change the %processLinked% value to the process name associated with the target service 
 
set servicename="explorerService"
set processLinked="explorer.exe"
set logfilename="C:\Logs\thisscript.log"
 
rem get the date and time
For /f "tokens=1-3 delims=/ " %%a in ('date /t') do (set mydate=%%c-%%b-%%a)
For /f "tokens=1-2 delims=/:" %%a in ('time /t') do (set mytime=%%a%%b)
 
rem execute the "sc query <service>" command and loop through the output
for /F "tokens=3 delims=: " %%i in ('sc query "%servicename%" ^| findstr " STATE"') do (
 
  rem log the datetime and service state to the logfile
  echo %mydate%_%mytime% >> %logfilename%
  echo "%servicename% Service's current state is: %%i" >> %logfilename%
 
  rem restart the service after killing off the associate %processLinked%
  echo "%servicename% Service is forcibly restarting..." >> %logfilename%
  taskkill /IM %processLinked% /F >> %logfilename%
  net start %servicename% >> %logfilename%
   
)
```
```