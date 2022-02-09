---
id: 716
title: 'Mac OSX Yosemite &#038; iCloud Failures'
date: '2016-09-16T15:09:32+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=716'
permalink: /2016/09/mac-osx-yosemite-icloud-failures/
categories:
    - 'MAC OSX'
tags:
    - bird
    - icloud
    - imac
    - osx
    - synchronization
---

### The Analysis

I received a report from an OSX Yosemite user who found documents saved on their iMac had stopped synchronizing to iCloud as they weren’t visible there or on the user’s MacAir.

Inspection showed the files in question had a grey dotted cloud next to their name in finder.

### The Tests

Documents created on the MacAir were synchronized back to the iMac so iCloud was working to some degree.

Creating a new document on the iMac resulted in the grey dotted cloud next to the document but nothing in the iCloud web interface.

Using the following command to inspect the “bird” daemon log indicated a fault with an alias file, locating that file I discovered it pointed to a non-existent file.

brctl log -w

I moved the broken alias out of the iCloud drive and the errors disappeared from the log but nothing appeared to be synchronizing.

I took a backup of the data (in addition to the Time Machine backup that is in permanent operation).

I then :

1. Stopped the “bird” daemon with “killall bird” on the terminall
2. Moved the “~/Library/Mobile\\ Documents” folder to the desktop (“~/Desktop/Mobile\\ Documents”)
3. Renamed the database store folder for the iCloud service “~/Library/Application\\ Support/CloudDocs/”
4. Moved the folder from step 2 (“~/Desktop/Mobile\\ Documents”) back into place at “~/Library/Mobile\\ Documents”
5. Rebooted the iMac and waited 12 hours (overnight).

The next day I inspected the machine and found around 40% of documents appeared to have re-synchronized, 10% had the dotted grey cloud and the remaining 50% had lost their file icon and instead had a dotted grey square for an icon!

I looked at Activity Monitor and inspected the “bird” process, it had read and written over 30GB of data to the disk, considering the user’s iCloud drive was around 3GB in use this seemed odd.

I restarted the iMac and waited a further 6 hours, upon returning all files had synchronized successfully and everything was well!