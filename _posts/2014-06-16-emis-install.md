---
id: 185
title: 'EMIS Install'
date: '2014-06-16T08:48:33+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=185'
permalink: /2014/06/emis-install/
categories:
    - Doctor
tags:
    - doctor
    - emis
    - nurse
    - vpn
---

1\. IT logs onto the PC with local admin privileges / runs the following installers with elevated privileges  
2\. Nurse logs onto https://vpn.oxnet.nhs.uk/ (the Nurse must login to “Oxfordshire-GP”) and downloads the VPN client  
3\. IT installs the VPN client on the target PC  
4\. The nurse connects to the VPN using his/her credentials  
5\. IT connects to ftp://213.146.154.199 (username and password required – available via phone from myself or EMIS support) and downloads “SDS 6 Install.exe”  
6\. IT installs “SDS 6 Install.exe” obtaining the nurses surgery site ID to complete the installation  
7\. The nurse logs into EMIS  
8\. IT completes the auto-updating of the software  
9\. IT logs off local admin / removes elevated privileges and disconnects EMIS and VPN  
10\. Nurse runs through the VPN connection and EMIS launch using their own user account