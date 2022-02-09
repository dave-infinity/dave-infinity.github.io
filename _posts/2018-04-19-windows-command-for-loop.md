---
id: 880
title: 'WIndows Command For-loop'
date: '2018-04-19T08:12:06+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=880'
permalink: /2018/04/windows-command-for-loop/
categories:
    - Microsoft
tags:
    - cmd
    - command
    - for
    - loop
---

```
for /f "delims=*" %f in ('dir "C:\folder\of\files\*.efs" /b') DO C:\folder\of\executable\program.exe -f "C:%~pf%f"
```

<div class="post-text">1. A standard debugging technique is to insert the `echo` command into scripts and even compound/complex commands. If you do ```
    for /f "delims=*" %a in ('dir *.avi /b /s') do @echo md "%~na"
    
    ```
    
    you’ll get the output
    
    ```
    "file 1"
    "file 2"
    "file 3"
    "file 4"
    
    ```
    
    Notes:
    
    
    - The **`@`** prevents the `echo` commands *themselves* from displaying, so you see only their output.
    - `"delims=…"` tells `for` how to parse the lines of output from the `dir *.avi /b /s` command. I don’t know why the answer you linked to suggests `"delims=*"`. But the default behavior is to break lines apart at spaces, so, if your directory and/or file names contain spaces (as you indicated), you should use `"delims="` (specifying that there are no delimiters) to get this to work.
2. If you type `for /?` or `help for`, you’ll get documentation on the `for` command. Down in the fifth page, you’ll see ```
    In addition, substitution of FOR variable references has been enhanced.
    You can now use the following optional syntax:
    
        %~I         - expands %I removing any surrounding quotes (")
                         ︙ 
        %~pI        - expands %I to a path only
        %~nI        - expands %I to a file name only
                         ︙ 
    
    The modifiers can be combined to get compound results …
                             ︙ 
    
    ```
    
    which explains why `%~na` is getting you just the file name of the `*.avi` files whose full names are in `%a`. Now try
    
    ```
    for /f "delims=" %a in ('dir *.avi /b /s') do @echo md "%~pa"
    
    ```
    
    and you’ll get
    
    ```
    "<i>the_current_directory</i>\Folder A\"
    "<i>the_current_directory</i>\Folder A\"
    "<i>the_current_directory</i>\Folder B\"
    "<i>the_current_directory</i>\Folder B\"
    ```
    
    From which we can conclude that you want to do
    
    ```
    for /f "delims=" %a in ('dir *.avi /b /s') do md "%~pa%~na"
    
    ```
    
    to create the `file 1` and `file 2` directories under `Folder A`, and the `file 3` and `file 4` directories under `Folder B`. And, as @dave\_thompson\_085 points out, you can combine `%~pa%~na` into `%~pna`.

</div><https://superuser.com/questions/1033360/how-do-i-execute-commands-on-files-in-multiple-folders>