---
id: 164
title: 'CMRS / Georgia'
date: '2014-03-17T10:48:23+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=164'
permalink: /2014/03/cmrs-georgia/
categories:
    - Uncategorized
tags:
    - cmrs
    - georgia
---

CMRS / GEORGIA:  
Step 1:  
look at importvisiting.pl (-h) on dc1-keble, note data type required (existing .csv’s from previous years visible in dc1-keblescriptscsv) – NOTE NO SPACE BETWEEN “,” and \[FirstName\]!!  
match provided data to this format, generating OWL credentials to finalise (use txt file for OWL generation including one name per line (surname,firstname middle(s))

STEP2:  
execute importvisiting.pl from dc1-keble using appropriate flags  
Now the data exists in local table

Step3:  
execute localimport.php twice on it.keble.ox.ac.uk  
this then creates entries in the card and people tables of the database

Step4:  
Back on dc1-keble execute \[user.pl -m -c\] to check (m) and commit (c) differences in the cars &amp; people tables to active directory, creating the new accounts.