---
id: 976
title: 'PowerShell : Delete Files Based on Path, Type &#038; Age'
date: '2019-11-18T09:16:18+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=976'
permalink: /2019/11/powershell-delete-files-based-on-path-type-age/
categories:
    - Powershell
tags:
    - powershell
    - remove-item
    - script
---

## Introduction 

 This script was created to clean up older IIS log files from a Windows IIS Server and is executed weekly on that server. It’s been written in as abstracted a manner as possible so could be used to delete any files in any target directory based on filetype and age by altering the variables.

## Input

None, although IIS log files are required somewhere on disk!

## Output 

<figure class="wp-block-table">| \# | Switches | Item | Description |
|---|---|---|---|
| 1 | None | Log | Log of files discovered and action(s) taken (if a file is deleted it will be recorded in the log). |

</figure>##  Logging 

Currently the logging is managed from within the script. The script currently resides on engs-svscc01.eng.ox.ac.uk and so the logging path variables have been designed to output within that server’s file system.

Log file location: **C:\\Logs\\DeleteIISLogFilesOlderThan.ps1.log**

$LOGTIME is s timestamp in the format “yyyy-MM-dd\_hh-mm-ss”

Log call within the script:   
“$LOGTIME &lt;&lt;TEXT TO LOG&gt;&gt;” | Out-File $LOG -Append -Force

The script is then contained with a try{} catch{} parameter with logging output for all exception messages and items.

I’ve also tried to log throughout each action within the script so both SUCCESS and ERRORs are logged which provides a debugging method (at least I should know where it falls over!).

## Usage Examples 

 Contained in the header of the script – see below

## The Script

```
<pre class="wp-block-code">```
# Name : DeleteIISLogFilesOlderThan.ps1
# Author : Dave 
# Date : 
# Ticket# : 
# version : 1.0
# Scope : Any directory defined by $TargetFolder, $filetype & $LastWrite defined by $Extension
#
# Input(s) : None
#
# Output(s) : Any files that match the $filetype in the $TargetFolder and are of $LastWrite age are logged in the $LOG and then deleted
#
# Usage Examples:
# PS> DeleteIISLogFilesOlderThan.ps1
 
 
########################
# Set the target variables for the folder, filetype and age
$Now = Get-Date
$Days = "<ENTER NUMBER OF DAYS HERE>"
$TargetFolder="<ENTER TARGET DIRECTORY HERE>"
$Extension = "*.log" # Change file type here
$LastWrite = $Now.AddDays(-$Days)
 
##########################
 
# Prepare the logging
##########################
# Check for the $LOGFILEDIR & $LOGFILENAME and create them if they don't exist
# NOTE: No logging until this happens except to STDOUT (Screen)
# Test for the folder and create if it doesn't exist:
 
$LOGFILEDIR = "C:\Logs" # the full path of the log file for the script to output to
$LOGFILENAME = "thisscriptlogfile.ps1.log" # the full name of the log file for the script to output to
$LOG = ($LOGFILEDIR + "\" + $LOGFILENAME)
$LOGTIME = Get-Date -Format "yyyy-MM-dd_hh-mm-ss"
 
Try
 {
 if(! (Test-Path -Path $LOGFILEDIR )){
 New-Item -ItemType directory -Path $LOGFILEDIR >$null
 }
 if(! (Test-Path $LOGFILEDIR\$LOGFILENAME )){
 New-Item -ItemType file -Path $LOGFILEDIR\$LOGFILENAME >$null
 }
 }
Catch
 {
 $ErrorMessage = $_.Exception.Message
 $FailedItem = $_.Exception.ItemName
 }
"$LOGTIME BEGIN STARTING SCRIPT" | Out-File $LOG -Append -Force
#########################
 
Try {
    if(Test-Path $TargetFolder )
    {
        $files = get-childitem -Path $TargetFolder -Include $Extension -Recurse | Where {$_.lastwritetime -lt "$LastWrite"}
        $filesFound = $false
        $files | Foreach-Object { $filesFound = $true }
 
        If($filesFound){
            "$LOGTIME  Non-Compliant, older files exist, removing and recording:" | Out-File $LOG -Append -Force
            foreach ($file in $files){
                "$LOGTIME  FILE DELETED : [$file.name]" | Out-File $LOG -Append -Force
                remove-item $file
            }
            "$LOGTIME SUCCESS Files deleted, exiting" | Out-File $LOG -Append -Force
        }
        Else
        {
            "$LOGTIME  Compliant, no files older than $($LastWrite) in $($TargetFolder) " | Out-File $LOG -Append -Force
        }
     }
     Else
     {
        #The Target Folder does not exists
        "$LOGTIME  Compliant, the folder $($TargetFolder) does not exist" | Out-File $LOG -Append -Force
     }
}
Catch
{
    $ErrorMessage = $_.Exception.Message
    $FailedItem = $_.Exception.ItemName
    "$LOGTIME ERROR $($ErrorMessage) $($FailedItem)" | Out-File $LOG -Append -Force #LOGACTION
}
```
```