---
id: 669
title: 'Silk, iSilk Wonderland'
date: '2016-07-22T08:26:25+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=669'
permalink: /2016/07/silk-isilk-wonderland/
categories:
    - Networking
tags:
    - isilk
    - query
    - silk
---

Notes on installing and using Silk network monitoring on a pre-configured log server named Wonderland

1. Download iSilk client from <https://tools.netsa.cert.org/isilk/download.html#>
2. Run the setup wizard and enter the FQDN of the wonderland server along with a valid username and passwordNOTE: I was unable to use the autoconfiguration tool in iSilk to connect to our server, it was failing to generate the SSH-DSA keys as intended so I used PuttyGen to create my own 2048-bit SSH-DSA keys and then copied the public key string to \[ ~/.ssh/authorized\_keys \] on the target server, ensuring I added to and not over-wrote the file.I could then skip the wizard and complete the Host, port, user(name), and public key file location on my local machine from the initial connection page and save that as the default.
3. On the \[General\] tab I entered:Output Directory = \[ /data/silk/dave \] , having created that dir on the server and applying the user:root permissions to it.  
    Library Path = \[ /data/silk/library \] , as defined in the silk.conf file (i think) on the target server.  
    Limit Maximum Records = \[UNTICK\]  
    Exclude IPv6 = \[TICKED\] (as our server doesn’t use it).
4. Using Putty’s \[ Pageant \] and loading in my private key file I was then able to launch iSilk and it connected cleanly to the target server!

Following the setup I then created my first set and within that my first query through the GUI which resulted in these options for the command line:

```
rwfilter --type=out,outweb,in,inweb --sensors=S1 --start-date=2016/07/18:18 --end-date=2016/07/19:01 --proto=0-255 --max-pass-records=0 --ip-version=4 --pass=FirstQuery.rwf --print-filenames
```