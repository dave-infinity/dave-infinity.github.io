---
id: 279
title: 'sed &#038; awk &#8211; Linux Tools, courses.edx.org'
date: '2014-09-24T07:28:30+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=279'
permalink: /2014/09/sed-linux-tools/
categories:
    - Linux
tags:
    - awk
    - 'command line'
    - linux
    - sed
    - terminal
---

| **Command** | **Usage** |
|:-:|:-:|
| sed s/pattern/replace\_string/ file | Substitute first string occurrence in a line |
| sed s/pattern/replace\_string/g file | Substitute all string occurrences in a line |
| sed 1,3s/pattern/replace\_string/g file | Substitute all string occurrences in a range of lines |
| sed -i s/pattern/replace\_string/g file | Save changes for string substitution in the same file |

| **Command** | **Usage** |
|:-:|:-:|
| awk ‘command’ var=value file | Specify a command directly at the command line |
| awk -f scriptfile var=value file | Specify a file that contains the script to be executed along with f |

| **Command** | **Usage** |
|:-:|:-:|
| awk ‘{ print $0 }’ /etc/passwd | Print entire file |
| awk -F: ‘{ print $1 }’ /etc/passwd | Print first field (column) of every line, separated by a space |
| awk -F: ‘{ print $1 $6 }’ /etc/passwd | Print first and sixth field |

\_