---
id: 141
title: 'Windows 2003+ domain &#8211; Prevent users adding computers to domain'
date: '2014-02-19T12:56:39+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=141'
permalink: /2014/02/windows-2003-domain-prevent-users-adding-computers-to-domain/
categories:
    - Microsoft
    - Server
    - Windows
tags:
    - 'active directory'
    - 'computer bind'
    - 'domain join'
    - 'micrsoft server'
---

1\. Open run and type ADSIEDIT.msc (may need to register adsiedit.dll on server first)

2\. Right click ADSIedit and choose connect to

3\. In the connection point section ,chose select A well Known Naming Context and ,from the drop-down list choose Default naming context

4\. Click OK

5\. Expand default naming context

6\. Right click the DC=mydomain,dc=local domain folder and choose properties

7\. Select ms-DS-MachineAccount Quta and click edit

8\. Type 0

9\. Click OK

<http://support.microsoft.com/kb/243327>