---
id: 981
title: 'Powershell : Module &#8211; Emailer'
date: '2019-11-18T13:28:15+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=981'
permalink: /2019/11/powershell-module-emailer/
categories:
    - Powershell
tags:
    - emailer
    - function
    - module
    - powershell
    - send-mailmessage
    - smtp
---

## Introduction 

 A small emailer module which can be used to send emails using a locally available SMTP server.

## Input

None

## Output 

An email is generated where a local SMTP server is available to route the email request

##  Logging 

None

## Usage Examples 

 Import the module to your script and then call it as per the example in the script

## Dependancies

None

## The Script

```
<pre class="wp-block-code">```
# Name      : Powershell Emailer when local SMPT available
# Author    : Dave 
# Date      : 
# Ticket#   : NONE
# Scope     : Power Shell Module, to the called by scripts
# Input(s)  : $emailFrom > [STR] > the sender's email address,
#             $emailTo   > [STR] > the target email addres,
#             $subject   > [STR] > the subject of the email 
#             $body  > [STR] > the email body
# Output(s) : An email is sent to the address specified.
#
# Example call:
# emailer "to@something.com" "from@somewhere.com" "email subject" "email body"
####################################################
 
# Notes:
########################
 
Function emailer ($emailTo, $emailFrom, $emailSubject, $emailBody)
<# This is a simple function that that sends an smtp email using the variables to define the email
i.e. "Function emailer ($emailFrom, $emailTo, $subject, $body) "
 
#>
 
{
$emailSmtpServer = "smtp.SOME.AVAILABLE.DOMAIN.COM"
Send-MailMessage -To $emailTo -From $emailFrom -Subject $emailSubject -Body $emailBody -SmtpServer $emailSmtpServer
}
```
```