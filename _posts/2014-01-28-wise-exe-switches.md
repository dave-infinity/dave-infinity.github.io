---
id: 102
title: 'Wise exe switches'
date: '2014-01-28T13:43:09+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=102'
permalink: /2014/01/wise-exe-switches/
categories:
    - Deployment
    - Microsoft
    - Windows
tags:
    - microsoft
    - switches
    - uninstall
    - unwise
    - windows
---

Ripped directly from [http://www.symantec.com/connect/blogs/wisescript-command-line-options](http://www.symantec.com/connect/blogs/wisescript-command-line-options "http://www.symantec.com/connect/blogs/wisescript-command-line-options")

**NOTE: I did find for Aleph that when running the uninstaller (unwise32.exe) I needed to use the shorthand C:Progra~1&lt;&lt;INSTALLDIR&gt;&gt;INSTALL.LOG syntax for it to find the log file.**

\[expand Title=”You can apply the following command line options to the WSE file. Command line options let you compile as well as set properties.”\]

/c file.wse  
Compiles the installation script.  
/c /s file.wse  
Compiles the installation script silently. You can use this option with the /d option.  
WiseScript Installations Command Line Options

You can apply the following command line options to compiled .EXE files.

/M  
Runs the installation in manual mode, prompting for system directories (examples: Windows, System).  
/M=filename  
Specifies a value file for installation.  
/S  
Installs in silent (automatic) mode with no end user choices.  
Uninstall Command Line Options

You can apply the following command line options to the WiseScript Express uninstall executable file, unwise.exe or unwise32.exe.

/Z  
Removes empty directories, including the one containing Unwise.  
/A  
Automatic mode. The Wise splash screen appears on the destination computer, and the uninstall proceeds immediately with no end user choices, except for questions about uninstalling shared files.  
/S  
Silent mode. The uninstall proceeds silently with no splash screen, no dialogs, and no end user choices.  
/R  
Rollback mode.  
/U  
Removes the Select Uninstall Method dialog, which means the end user does not see options for a custom, automatic, or repair uninstall.  
When you use command line options for the uninstall program, you must send it the path to the log file as a parameter. It must be the log file that is in the same folder as unwise.exe. If the path to the log file contains spaces, it must be surrounded by quotation marks.

Example:  
“C:Program FilesApplicationUNWISE.EXE” /A “C:Program FilesApplicationINSTALL.LOG” Application Uninstall\[/expand\]