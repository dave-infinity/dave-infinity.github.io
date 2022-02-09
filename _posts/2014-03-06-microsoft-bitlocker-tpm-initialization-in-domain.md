---
id: 152
title: 'Microsoft BitLocker TPM Initialization in Domain'
date: '2014-03-06T13:41:11+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=152'
permalink: /2014/03/microsoft-bitlocker-tpm-initialization-in-domain/
categories:
    - Windows
tags:
    - 'active directory'
    - bitlocker
    - domain
    - encryption
    - 'server 2008'
    - windows
---

First set the OU containers permissions to allow the NTSELF user of systems to write back TPM-ownerinformation, required when first initializing the TPM client:

1\. Open Active Directory Users and Computers.

2\. Select the OU where you have all computers which will have Bitlocker turned ON.

3\. Right Click on the OU and click Delegate Control.

4\. Click Next and then click Add.

5\. Type SELF as the Object Name.

6\. Select create a custom task to delegate.

7\. From the object in the folder, select Computer Objects.

8\. Under show these permissions, select all 3 checkbox.

9\. Scroll down in permissions and select the attribute Write msTPM-OwnerInformation.

10\. Click Finish.

11\. CUSTOM: Now add the computer to the AD Group named “bitlocker”

12\. CUSTOM: Finally power up client, turn on TPM and then initialize TPM in Windows

13\. CUSTOM: Enable bitlocker (must be logged in as local/domain admin) and check AD comp object for keys

Next follow the MS article on configuring AD / Bitlocker

[http://technet.microsoft.com/en-us/library/cc766015(v=ws.10).aspx](http://technet.microsoft.com/en-us/library/cc766015(v=ws.10).aspx  "http://technet.microsoft.com/en-us/library/cc766015(v=ws.10).aspx ")

To manage the keys you’ll need to register the BitLocker viewer from RSAT as detailed by MS here http://support.microsoft.com/kb/928202

Must be run as a domain admin: **regsvr32.exe BdeAducExt.dll**