---
id: 83
title: 'Windows Registry Key Permissions'
date: '2014-01-21T15:39:42+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=83'
permalink: /2014/01/windows-registry-key-permissions/
categories:
    - Microsoft
    - Registry
    - Windows
---

To take change ownership of registry keys in Windows use of the regini.exe tool seems simplest.

\[expand title=”MS KB 245031 describes using a script that regini.exe calls to execute, basically just the registry key referenced in a text file:”\]

```
Install the latest version of the Windows NT Server 4.0 Resource Kit.
Create a script file that contains the change commands:
Start any text editor (such as Notepad).
Type the registry keys and the appropriate permissions in the following format
Registryhivekey [permissions]
where hive is the name of the registry hive, key is the name of the registry key, and [permissions] is the binary number format of the permissions. 

For example, to modify the HKEY_LOCAL_MACHINESoftware registry key to give the Administrators group and the Creator/Owner group Full Control permission and the Everyone group Read permission, type the following string:
RegistryMachineSoftware [1 5 8]
NOTE: You must type the permissions in the binary number format. You must also refer to the registry hive in the predefined format. For more information about how to refer to a registry hive in a script file and about the binary numbers for various types of permissions, refer to the 'Reference to Registry Hives and Binary Number Representation for Permissions' section in this article.
Save and then close the script file.
Type the following command at a command prompt, and then press ENTER
REGINI [-m \computername] scriptname
where computername is the name of the computer and scriptname is the name of the script file you just created. 

NOTE: Use the -m option only when you edit the registry of a remote computer. Be sure to include the entire path to the script file.
Reference to Registry Hives and Binary Number Representation for Permissions 

Refer to registry hives as indicated below:
  HKEY_LOCAL_MACHINE - RegistryMachine
  HKEY_USERS - RegistryUsers
  HKEY_CURRENT_USER - RegistryUserUser_SID (where User_SID is the current user's security identifier)
```

\[/expand\]

[http://support.microsoft.com/Default.aspx?kbid=245031](http://support.microsoft.com/Default.aspx?kbid=245031 "http://support.microsoft.com/Default.aspx?kbid=245031")

\[expand title=”MS KB 237607 describes permissions levels:”\]

```
 1  - Administrators Full Access
 2  - Administrators Read Access
 3  - Administrators Read and Write Access 
 4  - Administrators Read, Write and Delete Access
 5  - Creator Full Access
 6  - Creator Read and Write Access
 7  - World Full Access
 8  - World Read Access
 9  - World Read and Write Access
 10 - World Read, Write and Delete Access
 11 - Power Users Full Access
 12 - Power Users Read and Write Access
 13 - Power Users Read, Write and Delete Access
 14 - System Operators Full Access
 15 - System Operators Read and Write Access
 16 - System Operators Read, Write and Delete Access
 17 - System Full Access
 18 - System Read and Write Access
 19 - System Read Access
 20 - Administrators Read, Write and Execute Access
 21 - Interactive User Full Access
 22 - Interactive User Read and Write Access
 23 - Interactive User Read, Write and Delete Access
```

\[/expand\]

[http://support.microsoft.com/?kbid=237607](http://support.microsoft.com/?kbid=237607 "http://support.microsoft.com/?kbid=237607")