---
id: 968
title: 'Powershell : Add $COMPUTERS to $GROUP'
date: '2019-11-18T08:55:57+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=968'
permalink: /2019/11/powershell-add-computers-to-group/
categories:
    - Microsoft
    - Powershell
tags:
    - 'active directory'
    - add-adgroupmember
    - groups
    - powershell
    - script
---

## Introduction 

 This script was created to add all computers in a given text file to a Windows AD security group

## Output 

 New objects are added the defined AD security group – check the variables in the script for the input file and target group  
 Local log file of events and errors on the executing computer C:\\Logs\\PowershellScripts\\add\_computers\_to\_group.ps1.log

##  Logging 

 Currently the logging is managed from within the script.  
 Log file location: C:\\Logs\\ADCudIncomingDisableAccounts\\cudincomingDisable.ps1.log  
 $LOGTIME is s timestamp in the format “yyyy-MM-dd\_hh-mm-ss”  
 Log call within the script:  
 “$LOGTIME &lt;&gt;” | Out-File $LOG -Append -Force  
 The script is then contained with a try{} catch{} parameter with logging output for all exception messages and items.  
 I’ve also tried to log throughout each action within the script so both SUCCESS and ERRORs are logged which provides a debugging method (at least I  
 should know where it falls over!).

## Usage Examples 

 Contained in the header of the script – see below  
 Dependancies  
 Powershell module “Import-Module ActiveDirectory”

## The Script

```
<pre class="wp-block-code">```
# Name        : Add Computers to Group
# Author    : Dave
# Date        : 
# Ticket#    :
# Scope     :  Text file containing computer names and an existing AD security group
# Input(s)    : text file with a list of computer names
# Output(s)    : 1. Log of script actions in csv to $LOGFILE
#                 2. Computers added to the specified AD security group
####################################################
# This script is designed to
# 1.  Add all computers in the $COMPUTERS text file to into $ADGROUP specified
####################################################
  
# Notes:
########################
  
  
# Set the variables
########################
$COMPUTERS = Get-Content -Path "ENTER AN ACCESSIBLE PATH TO A TEXT FILE OF COMPUTER NAMES, ONE PER LINE" # list of target computers
$GROUP = "ENTER A VALID AD SECURITY GROUP NAME TO TARGET"
 
$LOGFILEDIR = "C:\Logs\PowershellScripts\" # the full path of the log file for the script to output to
$LOGFILENAME =  "add_computers_to_group.ps1.log" # the full name of the log file for the script to output to
$LOG = ($LOGFILEDIR + "\" + $LOGFILENAME)
$LOGTIME = Get-Date -Format "MM-dd-yyyy_hh-mm-ss"
  
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
    }
  
  
"$LOGTIME BEGIN STARTING SCRIPT" | Out-File $LOG -Append -Force 
 
# Log the computer name in question
    # query ad for the computer and append the results to an array named $BITLOCKEDCOMPS
    Try
    {
        foreach ($COMPUTER in $COMPUTERS) {           
            $obj = Get-ADComputer $COMPUTER
            Add-ADGroupMember -ID $GROUP -Members $obj
            "$LOGTIME $($COMPUTER) ADDED TO $GROUP" | Out-File $LOG -Append -Force
         }
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $FailedItem = $_.Exception.ItemName
        "$LOGTIME ERROR $($_) Creating C:\$($TARGETDIR) $($ErrorMessage) $($FailedItem)" | Out-File $LOG -Append -Force
    }
      
    
 
      
"$LOGTIME END EXITING SCRIPT" | Out-File $LOG -Append -Force
exit
```
```