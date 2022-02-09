---
id: 255
title: 'Access VBA Loop'
date: '2014-07-23T11:29:03+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=255'
permalink: /2014/07/access-vba-loop/
categories:
    - Uncategorized
---

> [MS Access VBA – Looping through records](https://www.devhut.net/2010/06/12/ms-access-vba-looping-through-records/)

<iframe class="wp-embedded-content" data-secret="sPkwRRoNJJ" frameborder="0" height="327" marginheight="0" marginwidth="0" sandbox="allow-scripts" scrolling="no" security="restricted" src="https://www.devhut.net/2010/06/12/ms-access-vba-looping-through-records/embed/#?secret=sPkwRRoNJJ" style="position: absolute; clip: rect(1px, 1px, 1px, 1px);" title="“MS Access VBA – Looping through records” — DEVelopers HUT" width="580"></iframe>

```

Sub LoopRecExample()
On Error GoTo Error_Handler
Dim db As DAO.Database
Dim rs As DAO.Recordset
Dim iCount As Integer

Set db = CurrentDb()
Set rs = db.OpenRecordset("TableName") 'open the recordset for use (table, Query, SQL Statement)

With rs
If .RecordCount <> 0 Then 'Ensure that there are actually records to work with
'The next 2 line will determine the number of returned records
rs.MoveLast 'This is required otherwise you may not get the right count
iCount = rs.RecordCount 'Determine the number of returned records

Do While Not .BOF
'Do something with the recordset/Your Code Goes Here
.MovePrevious
Loop
End If
End With

rs.Close 'Close the recordset

Error_Handler_Exit:
On Error Resume Next
'Cleanup after ourselves
Set rs = Nothing
Set db = Nothing
Exit Sub

Error_Handler:
MsgBox "MS Access has generated the following error" & vbCrLf & vbCrLf & "Error Number: " & _
Err.Number & vbCrLf & "Error Source: LoopRecExample" & vbCrLf & "Error Description: " & _
Err.Description, vbCritical, "An Error has Occured!"
Resume Error_Handler_Exit
End Sub
```