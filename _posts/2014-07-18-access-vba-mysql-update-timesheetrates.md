---
id: 250
title: 'Access VBA > MySQL Update TimeSheetRates'
date: '2014-07-18T07:30:39+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=250'
permalink: /2014/07/access-vba-mysql-update-timesheetrates/
categories:
    - MySQL
tags:
    - 'microsoft access'
    - 'mysql update'
    - vba
---

Private Sub UpdateTimeSheetCalculations()  
On Error GoTo Err\_UpdateTimeSheetCalculations  
‘this simple subroutine looks at the MySQL View “time\_sheet\_calc\_dynamic” and copies the calculated values therein to the time\_sheet table  
‘The “time\_sheet\_calc\_dynamic” does not include records where the “ts\_calculation\_completed” column is set to 1. The DB Manager can switch this flag  
‘on and off via the Time Sheet Management form or when running a report for the timesheet. This means calculations made are “frozen in time”  
‘with the rates as they were so subsequent changes to mileage or on-call rates are not re-calculated.

Dim strSQLUpdate As String

 strSQLUpdate = “UPDATE time\_sheet AS x INNER JOIN time\_sheet\_calc\_dynamic AS y ON y.ts\_id = x.ts\_id SET ”

 strSQLUpdate = strSQLUpdate &amp; “x.ts\_MonMileage = y.MonMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_TueMileage = y.TueMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_wedMileage = y.wedMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_thuMileage = y.thuMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_friMileage = y.friMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_satMileage = y.satMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_sunMileage = y.sunMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_mamMileage = y.mamMileage,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_MonStandbyRate = y.MonStandbyRate,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_tueStandbyRate = y.tueStandbyRate,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_wedStandbyRate = y.wedStandbyRate,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_thuStandbyRate = y.thuStandbyRate,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_friStandbyRate = y.friStandbyRate,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_MonTotalHours = y.MonTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_tueTotalHours = y.tueTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_wedTotalHours = y.wedTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_thuTotalHours = y.thuTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_friTotalHours = y.friTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_satTotalHours = y.satTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_sunTotalHours = y.sunTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_mamTotalHours = y.mamTotalHours,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_MonMileageCosts = y.MonMileageCosts,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_tueMileageCosts = y.tueMileageCosts,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_wedMileageCosts = y.wedMileageCosts,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_thuMileageCosts = y.thuMileageCosts,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_friMileageCosts = y.friMileageCosts,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_satMileageCosts = y.satMileageCosts,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_sunMileageCosts = y.sunMileageCosts,”  
 strSQLUpdate = strSQLUpdate &amp; “x.ts\_mamMileageCosts = y.mamMileageCosts;”

CurrentDb.Execute strSQLUpdate, dbFailOnError

Exit\_UpdateTimeSheetCalculations:  
 Exit Sub  
Err\_UpdateTimeSheetCalculations:  
 MsgBox Err.description  
 Resume Exit\_UpdateTimeSheetCalculations  
End Sub