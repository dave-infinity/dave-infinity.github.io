---
id: 559
title: 'Google Sheets Image into Cell image(url)'
date: '2015-09-09T10:14:18+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=559'
permalink: /2015/09/google-sheets-image-into-cell-imageurl/
categories:
    - 'Google Docs'
    - Software
tags:
    - drive
    - 'google drive. google images'
    - 'google sheets'
    - images
    - sheets
---

Full credit to Eric Mercer via <http://googlesheetshelp.blogspot.fr/2014/11/method-for-displaying-images-stored-on.html>

The key to using images from Google Drive inside of a cell in a Google Sheets document is to check the sharing options apply to the viewer / owner of the google sheets and **reformat the url for the image**.

1. The containing folder and the image itself must be accessible by the Google Sheets document owner / viewer. ****They do not need to be public unless the google sheets document needs to be publicly viewable.****
2. Now get the shared URL for the image and reform it as indicated below: <div><div>```
    https://drive.google.com/open?id=0B9biAW_mGiSpQ1ZjWTNxLTE2RDQ&authuser=0
    ```
    
    </div></div><div>Becomes:</div><div><div>```
    http://drive.google.com/uc?export=view&id=0B9biAW_mGiSpQ1ZjWTNxLTE2RDQ
    ```
    
    </div></div>
3. Finally you can insert the following code into the Google Sheets cell to display the image: ```
    =image("http://drive.google.com/uc?export=view&id=0B9biAW_mGiSpQ1ZjWTNxLTE2RDQ", 1)
    ```
4. Options for image formatting thanks to <https://support.google.com/docs/answer/97447?hl=en>```
    To add an image inside of a cell, you can use the following formulas to change the size of the image in the cell. You must have a URL for the image you're adding.
    
    Size to fit: Type =IMAGE("URL") or =IMAGE("URL", 1) into the cell with the URL of the image you want to add. Using this formula will scale the image to fit inside of the selected cell. If the cell is bigger than the image you're inserting, the remainder of the cell will be white.
    Stretch to fit: Type =IMAGE("URL", 2) into the cell with the URL of the image you want to add.Using this formula will stretch the image to fit inside of the selected cell. The aspect ratio (height vs. width) of the image won't be preserved.
    Original size: Type =IMAGE("URL", 3) into the cell with the URL of the image you want to add. Using this formula will add the image into the cell at its original size. If the image is bigger than the cell, some of the image may be cut off.
    Custom size: Type =IMAGE("URL", 4, height, width) into the cell with the URL of the image you want to add, as well as your custom height and width (in pixels). Using this formula will add the image into the cell with your custom size.
    ```