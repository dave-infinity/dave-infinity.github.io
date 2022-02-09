---
id: 737
title: 'Deploying iTunes to Windows with Parental Controls'
date: '2016-12-14T12:11:43+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=737'
permalink: /2016/12/deploying-itunes-to-windows-with-parental-controls/
categories:
    - Apple
tags:
    - iTunes
    - 'itunes control'
    - 'itunes parental control'
    - 'itunes update'
    - update
---

### The Scene

We use WPKG to deploy Windows software within our domain and had a package to deploy iTunes (built from references here <https://wpkg.org/ITunes>) but wanted to prevent users from being pestered with iTunes update alerts (which they couldn’t install as non-admins anyway) whilst allowing them to update the iOS installations on their iPads and iPhones.

### The Hang ups

Reading the Apple guidance on parental controls <https://support.apple.com/en-gb/HT201677> was not terribly helpful, it was clear what flags were available and what values for those flags needed to be applied but the description of keys and DWORD values was not well defined.  
I spent some time trawling discussion threads and through a number of references worked out the correct interpretation of the Apple article.

### The Solution

In the “HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Apple Computer, Inc.\\iTunes\\Parental Controls\\Default” key we need a DWORD-32bit key with the name “kParentalFlags\_Locked” and a hex value of “1” (to prevent users from changing parental controls).

Inside the same parent key we need another DWORD-32bit value named “kParentalFlags\_DisableCheckForAppUpdates” with a hex-value of “200000” (to prevent iTunes from updating).

Finally we need another DWORD-32bit value in the same registry key named “AdminFlags” and it’s hex-value needs to be a SUM of all key values so far defined, in our case this is “200001”.

Including these keys in our deployment script means that the “check for updates” menu item in the “Help” menu is not present and iTunes does not check for updates for itself. It does leave the ability for users to check for updates for their iOS devices though.