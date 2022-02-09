---
id: 822
title: 'Plotting Multiple Postcodes on Google Maps'
date: '2018-01-16T20:04:23+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=822'
permalink: /2018/01/plotting-multiple-postcodes-on-google-maps/
categories:
    - random
---

### **Description of the task**

I received an Excel spreadsheet with a list of personal data including names, telephone numbers, membership numbers and addresses. I wanted to plot the addresses on a map in a way that left only the postcode identifiable for reasons of data protection as a postcode alone will not be traceable to more than a street it conforms with the requirements of being personally identifiable. Therefore the task required two stages to complete:

1. Anonymise personally identifiable data (offline on a secure computer)
2. Plot anonymised data on Google Maps

### **References**

My thanks to “Lisa in the Health Library” for her blog post which pointed me to Google Fusion Tables

### Anonymise personally identifiable data

To anonymise the data I created an additional column in the identifiable spreadsheet named “ID” and populated it with a contigious record count from 1 through to the last row and then saved the edited identifiable spreadsheet.  
I then created a second blank Excel spreadsheet (which I’ll refere to now as the anonymised spreadsheet) and copied both the postcode column and the newly created “ID” column from the identifiable spreadsheet into the anonymised spreadsheet and saved it under a new name.  
I now have a working anonymised spreadsheet which only I can identify the owners of the postcodes by referring back to the “ID” field in the identifiable spreadsheet if needed.

### **Plot anonymised data on Google Maps**

Using \*only\* the anonymised spreadsheet I then followed the guidance from “Lisa in the Health Library”‘s blogpost here: https://lisainthehealthlibrary.wordpress.com/2014/05/05/creating-google-maps-from-postcode-data/ and completed the mapping.