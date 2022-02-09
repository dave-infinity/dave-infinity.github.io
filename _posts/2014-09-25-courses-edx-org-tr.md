---
id: 296
title: 'courses.edx.org :  tr, tee, wc, cut'
date: '2014-09-25T08:16:23+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=296'
permalink: /2014/09/courses-edx-org-tr/
categories:
    - Linux
    - Uncategorized
tags:
    - cut
    - linux
    - tee
    - text
    - tr
    - wc
---

The **tr** utility is used to **translate** specified characters into other characters or to delete them. The general syntax is as follows:

$ tr \[options\] set1 \[set2\]

The items in the square brackets are optional. **tr** requires at least one argument and accepts a maximum of two. The first, designated set1 in the example, lists the characters in the text to be replaced or removed. The second, set2, lists the characters that are to be substituted for the characters listed in the first argument. Sometimes these sets need to be surrounded by apostrophes (or single-quotes (‘)) in order to have the shell ignore that they mean something special to the shell. It is usually safe (and may be required) to use the single-quotes around each of the sets as you will see in the examples below.

For example, suppose you have a file named city containing several lines of text in mixed case. To translate all lower case characters to upper case, at the command prompt type cat city | tr a-z A-Z and press the **Enter** key.

| **Command** | **Usage** |
|:-:|:-:|
| $ tr abcdefghijklmnopqrstuvwxyz ABCDEFGHIJKLMNOPQRSTUVWXYZ | Convert lower case to upper case |
| $ tr ‘{}’ ‘()’ &lt; inputfile &gt; outputfile | Translate braces into parenthesis |
| $ echo “This is for testing” \| tr \[:space:\] ‘t’ | Translate white-space to tabs |
| $ echo “This is for testing” \| tr -s \[:space:\] | Squeeze repetition of characters using -s |
| $ echo “the geek stuff” \| tr -d ‘t’ | Delete specified characters using -d option |
| $ echo “my username is 432234” \| tr -cd \[:digit:\] | Complement the sets using -c option |
| $ tr -cd \[:print:\] &lt; file.txt | Remove all non-printable character from a file |
| $ tr -s ‘n’ ‘ ‘ &lt; file.txt | Join all the lines in a file into a single line |

**tee: tee** takes the output from any command, and while sending it to standard output, it also saves it to a file. In other words, it “tees**”** the output stream from the command: one stream is displayed on the standard output and the other is saved to a file.

For example, to list the contents of a directory on the screen and save the output to a file, at the command prompt type ls -l | tee newfileand press the **Enter** key.

Typing cat newfile will then display the output of ls –l.

**wc wc** (word count) counts the number of lines, words, and characters in a file or list of files. Options are given in the table below.

By default all three of these options are active.

For example, to print the number of lines contained in a file, at the command prompt type wc -l filename and press the **Enter** key.

| **Option** | **Description** |
|:-:|:-:|
| –l | display the number of lines. |
| -c | display the number of bytes. |
| -w | display the number of words. |

**cut cut** is used for manipulating column-based files and is designed to extract specific columns. The default column separator is the **tab** character. A different delimiter can be given as a command option.

For example, to display the third column delimited by a blank space, at the command prompt type ls -l | cut -d” ” -f3 and press the **Enter** key.