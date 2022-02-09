---
id: 24
title: 'MySQL ODBC 5.2.6 Driver for Windows (2008 r2)'
date: '2013-11-21T15:31:32+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=24'
permalink: /2013/11/mysql-odbc-5-2-6-driver-for-windows-2008-r2/
categories:
    - Drivers
    - Microsoft
    - MySQL
    - Software
    - Windows
---

I was unable to install the x86 or x64 MySQL ODBC driver (v5.2.6) in my Windows 2008r2 server due to a reported missing module, the exact error was:

“Product: MySQL Connector/ODBC 5.2 — Error 1918.Error installing ODBC driver MySQL ODBC 5.2 ANSI Driver, ODBC error 13: The setup routines for the MySQL ODBC 5.2 ANSI Driver ODBC driver could not be loaded due to system error code 126: The specified module could not be found. (C:Program FilesMySQLConnector ODBC 5.2myodbc5S.dll).. Verify that the file MySQL ODBC 5.2 ANSI Driver exists and that you can access it.”

A little searching turned up a gem from another blogger, copying C:WindowsSystem32msvcr100\_clr0400.dll to C:WindowsSystem32msvcr100.dll and then restarting the MySQL driver installation worked a treat!

SOURCE: Thanks to Matt of [http://iwantanitcareer.com](http://iwantanitcareer.com "http://iwantanitcareer.com") for his reference in this fix!