---
id: 327
title: 'Outlook: Export all mail into Explorer'
date: '2014-10-30T12:04:52+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=327'
permalink: /2014/10/outlook-export-all-mail-into-explorer/
categories:
    - Microsoft
    - Software
tags:
    - archive
    - export
    - Outlook
---

This guide uses a VB script copied from <https://techniclee.wordpress.com/2013/05/09/export-outlook-folders-to-the-file-system/> as it’s basis.

The script here only copies emails from Outlook with no option for deleting the emails, for another layer of safety the deletion is left to the user to complete manually.

**The script will copy all emails from a selected folder, including subfolders, into Windows and retain each email’s attachments, sender and recipient addresses along with the timestamp information relating to the email (not the creation date within Windows).**

I’ve copied the edited script below for reference, thanks to the Keble IT Manager and a few of my own edits too I have a slightly improved version which handles errors better, this is available at the end of this article.

The process for importing this script to users is manual, thankfully only a handful of people require it so it’s not a huge overhead. The deployment process is:

From within Outlook:

1. Click \[File\] &gt; \[Options\] &gt; \[Customize Ribbon\] and \[TICK\] the \[Developer Ribbon\] check box, click \[OK\] to all open menus to close them
2. Click the \[Developer\] ribbon menu item &gt; \[Visual Basic\]
3. \[Insert\] &gt; \[Module\]
4. Copy and paste the script below into the window
5. Click the \[Save\] button and close the \[Visual Basic Window\] to return to Outlook
6. Click \[File\] &gt; \[Options\] &gt; \[Customize Ribbon\]
7. \[UN-TICK\] the \[Developer Ribbon\]
8. Click the \[New Tab\] button, highlight the \[New Tab (Custom)\] entry in the \[Main Tabs\] list &gt; click the \[Rename\] button &gt; Name the tab “Email Export”, click \[OK\] to save
9. Highlight the \[New Group (Custom)\] entry in the \[Main Tabs\] list &gt; click the \[Rename\] button &gt;Name the group “Export Highlighted Folder to Windows” &gt; Select an appropriate icon
10. In the left column, from the \[Choose commands from:\] drop-down menu select \[Macros\]
11. Click and drag the \[Project1.CopyOutlookFoldertoFileSystem\] entry onto the newly created new group named “Export Highlighted Folder to Windows”
12. Highlight the \[Project1.CopyOutlookFoldertoFileSystem\] entry in the \[Main Tabs\] list &gt; click the \[Rename\] button &gt;Name the command “Export”.
13. Click \[OK\] to close all open menus and return to Outlook

This creates a new tab with the script loaded into a single command named “Export” on the Outlook ribbon. The script doesn’t \*ever\* delete mail from Outlook, it only ever copies. To use the script:

1. Highlight a folder on the Outlook navigation pane that you want to copy to Windows
2. Click the new “Export” button
3. Select the Windows folder you want to export to
4. Click \[OK\] and wait for the export to complete, it may take a few minutes for 1GB+ folders
5. Once the transfer window disappears the copy is complete, inspect the folder in Windows to ensure the emails are there
6. Having double checked the export worked you can down delete the source folder from Outlook or all the emails inside it.

```
'On the next line edit the starting folder as desired. If you leave it blank, then the starting folder will be the local computer.
Const STARTING_FOLDER = ""
 
Dim objFSO As Object
 
Sub CopyOutlookFolderToFileSystem()
 ExportController "Copy"
End Sub
 
'Sub MoveOutlookFolderToFileSystem()
' ExportController "Move"
'End Sub
 
Sub ExportController(strAction As String)
 Dim olkFld As Outlook.MAPIFolder, strPath As String, dest As String
 strPath = SelectFolder(STARTING_FOLDER)
 If strPath = "" Then
 MsgBox "You did not select a folder. Export cancelled.", vbInformation + vbOKOnly, "Export Outlook Folder"
 Else
 Set objFSO = CreateObject("Scripting.FileSystemObject")
 Set olkFld = Application.ActiveExplorer.CurrentFolder
 ExportOutlookFolder olkFld, strPath
 If LCase(strAction) = "move" Then
 olkFld.Delete
 Else
 dest = strPath & "\" & olkFld.Name
 MsgBox "Now check that the right number of messages and folders are in " & dest & ", then delete the folder from Outlook"
 End If
 End If
 Set olkFld = Nothing
 Set objFSO = Nothing
End Sub
 
Sub ExportOutlookFolder(ByVal olkFld As Outlook.MAPIFolder, strStartingPath As String)
 Dim olkSub As Outlook.MAPIFolder, olkItm As Object, strPath As String, strMyPath As String, strSubject As String, intCount As Integer, s As String, d As Date, f As String, itemlist As Outlook.items
 
 On Error Resume Next
 ' Set an initial date just in case first item is broken
 d = Date
 strPath = strStartingPath & "\" & olkFld.Name
 objFSO.CreateFolder strPath
 ' Folder exists
 If Err.Number = 58 Then
 Dim rc As Integer
 rc = MsgBox("The folder " & strPath & " already exists, proceed anyway?", vbOKCancel)
 If rc = 1 Then
 Err.Clear
 Else
 Exit Sub
 End If
 End If
 
 Set itemlist = olkFld.items
 itemlist.Sort "[SentOn]", False
 
 For Each olkItm In itemlist
 ' Start with clean slate
 Err.Clear
 s = RemoveIllegalCharacters(olkItm.Subject)
 If Err.Number <> 0 Then
 s = "[Error in subject]"
 Err.Clear
 End If
 
 f = RemoveIllegalCharacters(olkItm.SenderName)
 If Err.Number <> 0 Then
 f = "[Error in sender]"
 Err.Clear
 End If
 ' This may fail in very rare circumstances. It'll use the date of the previous item as we've not reset it. That's probably close enough as the items are sorted into ascending date order.
 d = olkItm.SentOn
 
 strSubject = "[From] " & f & " [Subject] " & s
 strFilename = strSubject & ".msg"
 intCount = 0
 Do While True
 strMyPath = strPath & "\" & strFilename
 If objFSO.FileExists(strMyPath) Then
 intCount = intCount + 1
 strFilename = strSubject & " (" & intCount & ").msg"
 Else
 Exit Do
 End If
 Loop
 olkItm.SaveAs strMyPath, olMSG
 ChangeTimeStamp strMyPath, d
 Next
 For Each olkSub In olkFld.Folders
 ExportOutlookFolder olkSub, strPath
 Next
 Set olkFld = Nothing
 Set olkItm = Nothing
End Sub
 
Function SelectFolder(varStartingFolder As Variant) As String
 ' This function is a modified version of the SelectFolder function written by Rob van der Woude (http://www.robvanderwoude.com/vbstech_ui_selectfolder.php)
 
 ' Standard housekeeping
 Dim objFolder As Object, objShell As Object
 
 ' Custom error handling
 On Error Resume Next
 
 ' Create a dialog object
 Set objShell = CreateObject("Shell.Application")
 Set objFolder = objShell.BrowseForFolder(0, "Select the folder you want to export to", 0, varStartingFolder)
 
 ' Return the path of the selected folder
 If TypeName(objFolder) <> "Nothing" Then SelectFolder = objFolder.self.Path
 
 ' Standard housekeeping
 Set objFolder = Nothing
 Set objShell = Nothing
 On Error GoTo 0
End Function
 
Function RemoveIllegalCharacters(strValue As String) As String
 ' Purpose: Remove characters that cannot be in a filename from a string.'
 ' Written: 4/24/2009'
 ' Author: BlueDevilFan'
 ' Outlook: All versions'
 RemoveIllegalCharacters = strValue
 ' RemoveIllegalCharacters = LCase(RemoveIllegalCharacters)
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "<", "(")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, ">", ")")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, ":", "-")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, Chr(34), "'")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "/", "")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "\", "")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "|", "")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "?", "")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "*", "")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "+", "")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "@", "_at_")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, Chr(9), "")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "û", "u")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "ü", "u")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "à", "a")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "ç", "c")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "é", "e")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "è", "e")
 RemoveIllegalCharacters = Replace(RemoveIllegalCharacters, "ê", "e")
End Function
 
Sub ChangeTimeStamp(strFile As String, datStamp As Date)
 Dim objShell As Object, objFolder As Object, objFolderItem As Object, varPath As Variant, varName As Variant
 varName = Mid(strFile, InStrRev(strFile, "\") + 1)
 varPath = Mid(strFile, 1, InStrRev(strFile, "\"))
 Set objShell = CreateObject("Shell.Application")
 Set objFolder = objShell.NameSpace(varPath)
 Set objFolderItem = objFolder.ParseName(varName)
 objFolderItem.ModifyDate = CStr(datStamp)
 Set objShell = Nothing
 Set objFolder = Nothing
 Set objFolderItem = Nothing
End Sub

```