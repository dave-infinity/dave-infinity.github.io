---
id: 986
title: 'Powershell : Move Enabled Computers to Holding OU'
date: '2019-11-26T15:12:47+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=986'
permalink: /2019/11/powershell-move-enabled-computers-to-holding-ou/
categories:
    - Powershell
tags:
    - get-winevent
    - powershell
    - script
---

## Introduction 

This script loops through the $SourceOUs (a list of OUs from AD), identifies any enabled computers therein and moves them to the defined $TargetOU . It then emails $emailTo with a list of all affected computers and asks that the relevant IT teams are informed.

The reason for this action is to ensure that all bound and active computers fall under the scope of SCCM control which currently only affects machines within the prescribed OU structure.

**This is far from ideal but it’s a temporary fix.**

## Input

None

## Output 

An email is generated where a local SMTP server is available to route the email request

##  Logging 

Currently the logging is managed from within the script and will need to have the related variables customized to the script’s location.

$LOGTIME is s timestamp in the format “yyyy-MM-dd\_hh-mm-ss”

Log call within the script:   
“$LOGTIME &lt;&lt;TEXT TO LOG&gt;&gt;” | Out-File $LOG -Append -Force

The script is then contained with a try{} catch{} parameter with logging output for all exception messages and items.

I’ve also tried to log throughout each action within the script so both SUCCESS and ERRORs are logged which provides a debugging method (at least I should know where it falls over!).

## Usage Examples 

 Call the script, no parameters defined.

## Dependancies

 emailer.psm1

## The Script

```
<pre class="wp-block-code">```
# Name      : computerObjectManage
# Author    : Dave 
# Created   : 31/05/2019
# UPDATED   : 04/07/2019
# Version   : v2.0
# Ticket#   : XXXX
# Scope     : AD Computer Objects which are enabled and located in the AD OUs
# Input(s)  : None
# Output(s) : Log file of actions taken and an email to $emailTo if any computer objects were moved, including the account which bound them to the domain.
  
  
####################################################
# This script is designed to be located on [REDACTED] at  [REDACTED]  and run with user rights to move computer objects from the  [REDACTED] 
# It will be called nightly via a Scheduled Task defined on the server.
#
# 1. Identify all computer objects in AD which are enabled and which exist in either the OU
# 2. Parse the event logs on all Domain Controllers for Event ID 4741 and record the computername and username of the binder
# 3. Log those computer names, distinguished names, descriptions and username of the binder to a log file
# 4. Move those computer objects to the $TargetOU
# 5. Email $emailTo with a list of the computers moved, the username who bound them, the computer's distinguished names and their descriptions.
####################################################
  
# Variables:
# Files
$LOGFILEDIR = "<<INPUTE LOGFILE DIR HERE>>" # the full path of the log file for the script to output to
$LOGFILENAME =  "computerObjectManage.ps1.log" # the full name of the log file for the script to output to
$LOG = ($LOGFILEDIR + "\" + $LOGFILENAME)
$LOGTIME = Get-Date -Format "yyyy-MM-dd_hh-mm-ss"
  
# Text Strings
$SourceOUs =  [REDACTED] 
$TargetOU =  [REDACTED] 
$emailer = "<<FULL PATH OF emailer.psm1 HERE>>"
 
# eventlog querying variables
$domain = "you.domain.com"
$dcou =  [REDACTED] 
$dcs = get-adcomputer -filter * -properties name -searchbase $dcou | select name
# set the hashtable variable to record the eventlog results from the domain controllers
$domainBindEvents = @{}
  
# Email settings
$emailTo = "your@email.com"
$emailFrom = "yourscript@email.com"
  
# Email subject and the first section of the body
$subject_output =  [REDACTED] 
  
Import-Module -Name $emailer #-Verbose
  
# Prepare the logging
##################################################################################
# Check for the $LOGFILEDIR & $LOGFILENAME and create them if they don't exist
# NOTE: No logging until this happens except to STDOUT (Screen)
# Test for the folder and create if it doesn't exist:
##################################################################################
  
Try
    {
      
        if(! (Test-Path -Path $LOGFILEDIR )){
                New-Item -ItemType directory -Path $LOGFILEDIR
            }
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
  
  
##################################################################################
# Main
##################################################################################
  
Try
    {
        # Using the list of $SourceOUs (defined at the start of this script) loop through each OU and add any computers' distinguished names and which are ENABLED to the $targetcomps array.
        $targetcomps = foreach ($OU in $SourceOUs) { get-adcomputer -filter {enabled -eq "True"} -properties Name, DistinguishedName, Description -SearchBase "$OU" | select DistinguishedName, Name, Description}
        # test to see if there were any computers discovered and added to the $targetcomps array by inspecting it's length.
        # If computers were discovered then continue, else log that there weren't and exit the script.
          
        if ($targetcomps.length -eq 0) {
            "$LOGTIME COMPLETED No computers were discovered in $($SourceOUs)" | Out-File $LOG -Append -Force
            exit
            #write-host "no targetcomps"
        }
        else {
            # If there were computers in the default OUs:
             
            # Check the event logs on all DC's for the event ID 4741 in the Security eventlog and
            # add any entries' computer name and account which bound it to the the hashtable $domainBindEvents
            try {
             
                foreach ($dc in $dcs){
                 
                    # Loop through each DC in the $dcou OU and for each one:
                    # Set the FQDN to $dcfqdn
                    $dcfqdn = $dc.name + $domain
                     
                    try{
                     
                        # Add all events matching 4741 from the Security event log to the $dc4741events hashtable
                        "$LOGTIME INFO querying $($dcfqdn) for 4741 events..." | Out-File $LOG -Append -Force
                        $dc4741events += get-winevent -computername $dcfqdn -FilterHashtable @{logname='security';id=4741}
                    }
                    catch
                    {
                        # if there were no events continue to the next DC
                        $ErrorMessage = $_.Exception.Message
                        $FailedItem = $_.Exception.ItemName
                        "$LOGTIME ERROR $($ErrorMessage) $($FailedItem)" | Out-File $LOG -Append -Force #LOGACTION
                        continue
                    }
                     
                    # If events were found then:
                    if ($dc4741events) {
                     
                        foreach ($event in $dc4741events){
                                         
                            # expand the event and assign the 8th item to $computername and the 4th to $userwhobound
                            $computername = $event.Properties[8]
                            $userwhobound = $event.Properties[4]
                             
                            # Update the hashtable $domainBindEvents with the new values
                            $domainBindEvents[$computername.value.SubString(0,$computername.value.Length-1)] = $userwhobound.value
                            "$LOGTIME INFO Events Found on $($computername.value.SubString(0,$computername.value.Length-1)) bound by $($userwhobound.value) " | Out-File $LOG -Append -Force
                        }
                    }
                }
 
            }
            catch
            {
                $ErrorMessage = $_.Exception.Message
                $FailedItem = $_.Exception.ItemName
                "$LOGTIME ERROR $($ErrorMessage) $($FailedItem)" | Out-File $LOG -Append -Force #LOGACTION
            }
             
            # Loop through the list of computers which were discovered in a default OU
            foreach ($comp in $targetcomps) {
             
                # Loop through the $boundcompevents.keys
                foreach ($boundcompevent in $domainBindEvents.keys){
                    #write-host "$($boundcompevent)"
                    # Compare the $comp with the key values of the $domainBindEvents to see if there's a match:
                    #write-host "DOES $($boundcompevent) EQUAL $($comp.Name.tolower())?  "
                    if ($boundcompevent.tolower() -eq $comp.Name.tolower()){
                        #write-host true
                        # If there is a match then:
                        # Assign the username of the account which bound the matching computer to the domain and break out of this sub-forloop
                        $usernamebinder = $domainBindEvents.$boundcompevent
                        break
                    }
                    else
                    {
                        #write-host false
                        # If no matching computer was identified in the event log IDs 4741 assign the fixed string to the $usernamebinder requesting the receiver of the email alert investigate.
                        $usernamebinder = "UNKNOWN, could not identify a user from the 4741 event ID's on the DCs - manual identification required"
                        #Log the
                        "$LOGTIME INFO No matching event log for binding $($comp.name.tolower()) - it didn't match $($boundcompevent.tolower())"| Out-File $LOG -Append -Force
                    }
                }
                 
                # Move the Computer Object to the $TargetOU
                move-adobject -identity $comp.DistinguishedName  -targetpath $TargetOU  
                  
                #Log the move computer object action
                "$LOGTIME INFO $($comp.Name) LOCATED AT $($comp.DistinguishedName) WAS MOVED TO THE _WindowsClients\WindowsClientsNeedOURelocation OU"| Out-File $LOG -Append -Force
                 
                # Add the computer name, distinguishedName, Description and the username of the person who bound the computer to the domain to the email body
                $body_output_complist += "`n" + "COMPUTER_NAME = " + $comp.Name +  "    USERNAME_THAT_BOUND_COMPUTER = " + $usernamebinder +  "    COMPUTER_DESCRIPTION = " + $comp.Description +  "    COMPUTER_DISTINGUISHED_NAME=" + $comp.DistinguishedName + "`n"
            }
                          
        #Email the results
        $body = $body_output + " " + $body_output_complist
        "$LOGTIME INFO Sending email to $($emailTo) reporting the computers that were discovered and moved ....  "| Out-File $LOG -Append -Force
        emailer $emailTo $emailFrom $subject_output $body
        "$LOGTIME SUCCESS Email sent  "| Out-File $LOG -Append -Force         
        "$LOGTIME FINISH The script has completed  "| Out-File $LOG -Append -Force
         
        }
    }
Catch
    {
        $ErrorMessage = $_.Exception.Message
        $FailedItem = $_.Exception.ItemName
        "$LOGTIME ERROR $($ErrorMessage) $($FailedItem)" | Out-File $LOG -Append -Force #LOGACTION
        exit
    }
```
```