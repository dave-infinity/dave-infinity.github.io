---
id: 129
title: 'VBScript &#038; Fonts on Windows 7'
date: '2014-02-04T09:59:09+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=129'
permalink: /2014/02/vbscript-fonts-on-windows-7/
categories:
    - Microsoft
    - 'VB Script'
tags:
    - Fonts
    - vb
    - vbscript
    - 'visual basic'
---

Some VBScript pulled from experts-exchange.com.

This sub routine takes two inputs, filename (registry name of Font as found in  
\[HKLMSoftwareMicrosoftWindows NTCurrentVersionFonts\]  
) and the fully qualified filename of the font on the system and then deletes them both:

```
Remove_Font "Helvectiva XXXXXXXX", "c:windowsfontsHELNLTPR.TTF"

Sub Remove_Font(strFontName, strFile)

	Set oFSO = CreateObject("Scripting.FileSystemObject")
 	Set oShell = CreateObject("WScript.Shell")
	' If the file exists
	If oFSO.FileExists(strFile) Then
		' Delete the file
		oFSO.DeleteFile strFile, True
		On Error Resume Next
		oShell.RegDelete "HKLMSoftwareMicrosoftWindows NTCurrentVersionFonts" & strFontName
		If Err.Number = 0 Then
			MsgBox strFile & " was removed."
		Else
			MsgBox strFile & " was deleted, but the registry key still exists."
		End If
		Err.Clear
		On Error GoTo 0
	Else
		MsgBox strFile & " was not found."
	End if

	Set oFSO = Nothing

End Sub
```