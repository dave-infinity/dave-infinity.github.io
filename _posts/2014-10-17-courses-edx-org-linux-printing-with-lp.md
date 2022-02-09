---
id: 308
title: 'courses.edx.org: Linux Printing with lp'
date: '2014-10-17T08:14:49+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=308'
permalink: /2014/10/courses-edx-org-linux-printing-with-lp/
categories:
    - Linux
tags:
    - enscript
    - linux
    - lp
    - pinting
---

**Using lp**

**lp** and **lpr** accept command line options that help you perform all operations that the GUI can accomplish. **lp** is typically used with a file name as an argument.

Some **lp** commands and other printing utilities you can use are listed in the table.

| **Command** | **Usage** |
|:-:|:-:|
| lp &lt;filename&gt; | To print the file to default printer |
| lp -d printer &lt;filename&gt; | To print to a specific printer (useful if multiple printers are available) |
| program \| lp   echo string \| lp | To print the output of a program |
| lp -n number &lt;filename&gt; | To print multiple copies |
| lpoptions -d printer | To set the default printer |
| lpq -a | To show the queue status |
| lpadmin | To configure printer queues |

The **lpoptions** utility can be used to set printer options and defaults. Each printer has a set of **tags** associated with it, such as the default number of copies and authentication requirements. You can execute the command lpoptions help to obtain a list of supported options. **lpoptions** can also be used to set system-wide values, such as the default printer.

| **Command** | **Usage** |
|:-:|:-:|
| lpstat -p -d | To get a list of available printers, along with their status |
| lpstat -a | To check the status of all connected printers, including job numbers |
| cancel job-id   OR   lprm job-id | To cancel a print job |
| lpmove job-id newprinter | To move a print job to new printer |

**Working with enscript**

**enscript** is a tool that is used to convert a text file to PostScript and other formats. It also supports **Rich Text Format (RTF)** and **HyperText Markup Language (HTML)**. For example, you can convert a text file to two column (-2) formatted **PostScript** using the command: enscript -2 -r -p psfile.ps textfile.txt. This command will also rotate (-r) the output to print so the width of the paper is greater than the height (aka landscape mode) thereby reducing the number of pages required for printing.

The commands that can be used with **enscript** are listed in the table below (for a file called ‘textfile.txt’).

| **Command** | **Usage** |
|:-:|:-:|
| enscript -p psfile.ps textfile.txt | Convert a text file to PostScript (saved to psfile.ps) |
| enscript -n -p psfile.ps textfile.txt | Convert a text file to n columns where n=1-9 (saved in psfile.ps) |
| enscript textfile.txt | Print a text file directly to the default printer |