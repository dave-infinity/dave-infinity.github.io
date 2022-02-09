---
id: 978
title: 'PowerShell : DHCP Log Backup Script'
date: '2019-11-18T13:22:34+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=978'
permalink: /2019/11/powershell-dhcp-log-backup-script/
categories:
    - Powershell
tags:
    - copy-item
    - powershell
    - script
---

## Introduction 

 This script is designed to backup DHCP logs from a Windows DHCP Server to another location.

## Input

<figure class="wp-block-table">| Inputs | Type |
|---|---|
| A text file with a list of target computer names, one per line. | Variable assignment within the script |

</figure>## Output 

<figure class="wp-block-table">| outputs | Type | Item | Description |
|---|---|---|---|
| Copy of DHCP Logs | File(s) | Log | defined by the script |

</figure>##  Logging 

 Logging is basic for now, a log file is defined within the script by the controlling variables at the top and it logs all errors and successes from each command within the script.

## Usage Examples 

To call this script:

1. Ensure the variables under the heading “Set the variables” are configured for
    1. A valid scriptlog directory
    2. A valid input file listing the target DHCP servers, one per line
2. Ensure the target DHCP servers’s dhcp log directory is available to the calling security principal

## Dependancies

 emailer.psm1 module : [https://www.oxfordshirecomputing.co.uk/powershell-module-emailer/ ](https://www.oxfordshirecomputing.co.uk/powershell-module-emailer/)

The Script

```
<pre class="wp-block-code">```
# Name      : Windows DHCP Log Backup
# Last Edit : 
# Author    : Dave 
# Date      : 
# Ticket#   :
# Scope     : All Windows DHCP Servers
# Inputs    : none
# Output(s) : Log of script actions in csv to $LOGFILE, targeted log files moved from the host server to the TARGET SERVER server.
 
####################################################
# This script is designed to take a list of DHCP server names or IP addresses as an input from an external text file via the
# $Computers variable and copy the previous day's DHCP logs from that server to the target backup server
# \\SERVER\Windows\DHCP\, creating a sub directory within that share in the DNS name or IP address of the DHCP server,
# leaving the original logs in place at source.
####################################################
 
# Notes:
########################
# To call this script:
# 1. Ensure the variables under the heading "Set the variables" are configured for
#    - A valid scriptlog directory
#    - A valid input file listing the target DHCP servers, one per line
# 2. Ensure the local dhcp folder is shared with read permissions for the calling principal (account) and has read file permissions enabled for that account.
# 3. Call the script via powershell, no arguments required.
 
# Set the variables
########################
# Log file variables
$LOGFILEDIR = "C:\scripts\Powershell\PSScriptLogs" # the full path of the log file for the script to output to
$LOGFILENAME =  "dhcplogbackup.ps1.log" # the full name of the log file for the script to output to
$LOG = ($LOGFILEDIR + "\" + $LOGFILENAME)
$LOGTIME = Get-Date -Format "MM-dd-yyyy_hh-mm-ss"
 
# Script variables
$Computers = Get-Content -Path "C:\scripts\Powershell\PSScriptInputs\dhcpservers.txt" # list of target computers
$dateYesterday = get-date -date $(get-date).adddays(-1) -format "MM/dd/yyyy"
$filedate =  get-date -date $(get-date).adddays(-1) -format "yyyy-MM-dd"
$today = get-date -format "MM/dd/yyyy"
$logdir = "Windows\System32\dhcp" #define the target log directory to be backed up / moved
# variables for the current computer -- > See below
 
 
# Email settings
$emailer = "C:\scripts\Powershell\Modules\emailer.psm1"
$emailTo = "it-alerts@something.com"
$emailFrom = "DHCPLogBackup@something.com"
# Email subject and the first section of the body
$subject_output = "DHCP Log Copy Script"
$body = "Ref: SOMEREF `n`nThe DHCP Log File backup script encountered an error. `n`nPlease complete the following actions:
`n`n
1. Log a ticket to record this alert and your response
`n
2. Visit the script execution server and examine the C:\Logs\dhcplogbackup.ps1.log file for clues
`n
3. Either correct the fault and re-run the script or manually copy the target DHCP logs which failed from \Windows\System32\Logs\DHCP\ to \\SERVER\Windows\DHCP\<SERVERNAME>\ and await the overnight scheduled re-run of the script
`n`n
This script runs to ensure we can retain a 90 day log of DHCP lease activity for our domain, it is critical in that regard until a centralised logging system has been established.
`n`n
Thanks.`n`n Dave
"
 
# Imported modules
Import-Module -Name $emailer #-Verbose
 
# Prepare the logging
##########################
# Check for the $LOGFILEDIR & $LOGFILENAME and create them if they don't exist
# NOTE: No logging until this happens except to STDOUT (Screen)
# Test for the folder and create if it doesn't exist
Try
    {
     
        if(! (Test-Path -Path $LOGFILEDIR )){
                New-Item -ItemType directory -Path $LOGFILEDIR
            }
    }
Catch
    {
        $ErrorMessage = $_.Exception.Message
        $FailedItem = $_.Exception.ItemName
        emailer $emailTo $emailFrom $subject_output "DHCP LOG BACKUP SCRIPT FAILED TO CREATE LOCAL SCRIPT LOGFILE!"
    }
     
# test for the file and create if it doesn't exist
Try
    {
        if(! (Test-Path $LOGFILEDIR\$LOGFILENAME  )){
            New-Item -ItemType file -Path $LOGFILEDIR\$LOGFILENAME
        }
    }
Catch
    {
        $ErrorMessage = $_.Exception.Message
        $FailedItem = $_.Exception.ItemName
        emailer $emailTo $emailFrom $subject_output "DHCP LOG BACKUP SCRIPT FAILED TO CREATE LOCAL SCRIPT LOGFILE!"
    }
     
"$LOGTIME BEGIN STARTING SCRIPT" | Out-File $LOG -Append -Force
 
# BODY
##########################
# Loop through the list of computers
$Computers | Foreach-Object {
     
    # Log the computer name in question
    "$LOGTIME START $($_)" | Out-File $LOG -Append -Force
     
    # variables for the current computer
    $hostname = $($_) # The current server's hostname
    $sourceLogs = "\\$hostname\dhcp" # the location of the DHCP logs ($logdir) on the current computer
    $targetdir = "\\SERVER FQDN\Windows\DHCP\$($hostname)" # Target dir on some server for current server
    $targetparent = split-path $targetdir # Parent dir of the target dir on some server for current server
     
    #Test access to the sourceLogs directory, if this fails log the failure and exit (the script can't copy from non-existent targets)
    try {
        if (test-path $sourceLogs -isvalid) {
            Try {
                # collect all filenames into the $files variable which begin with "Dhcp" and end with ".log" and which have a LastAccessTime value for yesterday
                $files = get-childitem $sourceLogs | where-object {($_.name -like "Dhcp*.log") -and ($_.LastAccessTime -ge $dateYesterday) -and ($_.LastAccessTime -lt $today)} | select name
            }
            catch{
                $ErrorMessage = $_.Exception.Message
                $FailedItem = $_.Exception.ItemName
                "$LOGTIME ERROR $($_) Unable to get-childitem for $($sourceLogs) $($ErrorMessage) $($FailedItem) " | Out-File $LOG -Append -Force
                emailer $emailTo $emailFrom $subject_output $body
                "$LOGTIME SUCCESS Email Alert Sent"| Out-File $LOG -Append -Force        
                "$LOGTIME FINISH The script has completed  "| Out-File $LOG -Append -Force
            }
             
            # check that files were found, if not generate an email alert for review of this script
            if (!($files)) {
                "$LOGTIME ERROR No files were located by the script : $($files) Review the logfile $($LOG) for clues - ensure the backup is completed!" | Out-File $LOG -Append -Force
                emailer $emailTo $emailFrom $subject_output $body
                "$LOGTIME FAIL Email Alert Sent"| Out-File $LOG -Append -Force        
                "$LOGTIME FINISH The script has completed  "| Out-File $LOG -Append -Force
            }
            }
             
             
            #Check the path \\SERVER\Windows\ contains a folder using this server's hostname, if not then create one.
            If (!(test-path $targetdir)) {
                Try {
                    New-Item -Path $targetparent -Name $hostname -ItemType "directory"
                }
                Catch {
                    $ErrorMessage = $_.Exception.Message
                    $FailedItem = $_.Exception.ItemName
                    "$LOGTIME ERROR $($_) Creating $($targetparent)\$($hostname) $($ErrorMessage) $($FailedItem)" | Out-File $LOG -Append -Force
                    emailer $emailTo $emailFrom $subject_output $body
                    "$LOGTIME FAIL Email Alert Sent"| Out-File $LOG -Append -Force        
                    "$LOGTIME FINISH The script has completed  "| Out-File $LOG -Append -Force
                }
            }
             
            #Copy the yesterday's DHCP log file into the target directory, prefixing the date to the filename
            Foreach ($file in $files) {
                try {
                    $fileName = $file.name
                    #write-host $fileName
                    copy-item $sourceLogs\$fileName -destination $targetdir\$filedate"-"$fileName
                }
                Catch {
                    $ErrorMessage = $_.Exception.Message
                    $FailedItem = $_.Exception.ItemName
                    "$LOGTIME ERROR $($_) executing copy-item or remove-item against $($sourceLogs)\$($fileName) : $($ErrorMessage) $($FailedItem)" | Out-File $LOG -Append -Force                 
                    emailer $emailTo $emailFrom $subject_output $body
                    "$LOGTIME FAIL Email Alert Sent"| Out-File $LOG -Append -Force        
                    "$LOGTIME FINISH The script has completed  "| Out-File $LOG -Append -Force
                }          
            }
        }  
        Catch {
        $ErrorMessage = $_.Exception.Message
        $FailedItem = $_.Exception.ItemName
        "$LOGTIME ERROR $($_) the $($sourceLogs) path was not found - no action taken, exiting..." | Out-File $LOG -Append -Force
        emailer $emailTo $emailFrom $subject_output $body
        "$LOGTIME FAIL Email Alert Sent"| Out-File $LOG -Append -Force        
        "$LOGTIME FINISH The script has completed  "| Out-File $LOG -Append -Force
    }
}
```
```