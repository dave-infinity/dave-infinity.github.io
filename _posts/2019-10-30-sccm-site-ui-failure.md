---
id: 955
title: 'SCCM Site Console (Admin UI) Failure'
date: '2019-10-30T12:03:02+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=955'
permalink: /2019/10/sccm-site-ui-failure/
categories:
    - SCCM
tags:
    - adminUi
    - console
    - sccm
---

Following a number of interferences with our beloved SCCM Primary Site it was in a broken state.  
  
The “\\Program Files\\Microsoft Configuration Manager\\AdminConsole\\AdminUILog\\SmsAdminUI.log” reported:  
  
 “Error Code:  
ProviderLoadFailure  
\\r\\nSystem.Management.ManagementException\\r\\nProvider load failure \\r\\n at System.Management.ManagementException.ThrowWithExtendedInfo(ManagementStatus errorCode)  
 at System.Management.ManagementObjectCollection.ManagementObjectEnumerator.MoveNext()  
 at Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine.WqlQueryResultsObject.&lt;GetEnumerator&gt;d\_\_74.MoveNext()\\r\\nManagementException details:  
instance of \_\_ExtendedStatus  
{  
 Operation = “ExecQuery”;  
 ParameterInfo = “SELECT \* FROM SMS\_Site WHERE SiteCode = ‘XXX'”;  
 ProviderName = “WinMgmt”;  
};  
”

Where “XXX” is the name of an SCCM site but not ours! This led me to https://docs.microsoft.com/en-us/previous-versions/system-center/configuration-manager-2007/bb633148(v=technet.10)?redirectedfrom=MSDN followed by https://docs.microsoft.com/en-us/previous-versions/system-center/configuration-manager-2007/bb932190(v=technet.10)?redirectedfrom=MSDN , this latter article walked me through examinig the SMS\_Providor WMI class and it is there I found the spurious reference to the unknown XXX site.  
  
Deleting that reference restored AdminUI Console functionality (yay!).

Another case with similar symptoms was the result of a WMI db corruption which caused the OS to automatically rebuild the db but which did not re-import the SCCM WMI references. That was resolved by:

1. Run &gt; Wbemtest
2. Connect to “root\\sms” –&gt; Enum Classes–&gt;Select recursive and check for SMS\_ProviderLocation – it was not present
3. From an elevated command prompt enter the following commands to add the SCCM .mof’s (excluding the \_\*.mofs) to the $mofs variable and then switch to the Wbem folder and import the WMI modules to the OS `PS D:\> $mofs = get-childitem "D:\Program Files\Microsoft Configuration Manager\bin\X64" -filter "*.mof" -exclude "_*.mof" -recurse``PS D:\> cd C:\Windows\System32\Wbem``PS C:\Windows\System32\Wbem> foreach ($mof in $mofs){mofcomp $mof.FullName}`
4. Restart the Windows Management Instrumentation Service
5. Repeated Steps#1 &amp; 2 and noted SMS\_ProviderLocation now exists in WMI
6. Launched SCCM Admin Console locally successfully
7. Launched SCCM Admin Console remotely successfully
8. Launched Task Sequence Creation Wizard successfully