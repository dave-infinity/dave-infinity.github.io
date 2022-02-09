---
id: 292
title: 'courses.edx.org : regex'
date: '2014-09-24T08:01:50+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=292'
permalink: /2014/09/courses-edx-org-regex/
categories:
    - Linux
tags:
    - regex
    - 'regular expressions'
---

| **Metacharacter** | **Description** |
|:-:|:-:|
|  | Specifies the next character as either a special character, a literal, a back reference, or an octal escape. |
| **^** | Matches the position at the beginning of the input string. |
| **$** | Matches the position at the end of the input string. |
| **\*** | Matches the preceding subexpression zero or more times. |
| **+** | Matches the preceding subexpression one or more times. |
| **?** | Matches the preceding subexpression zero or one time. |
| **{n}** | Matches exactly n times, where n is a non-negative integer. |
| **{n,}** | Matches at least n times, n is a non-negative integer. |
| **{n,m}** | Matches at least n and at most m times, where m and n are non-negative integers and n &lt;= m. |
| **.** | Matches any single character except “n”. |
| **\[xyz\]** | A character set. Matches any one of the enclosed characters. |
| **x\|y** | Matches either x or y. |
| **\[^xyz\]** | A negative character set. Matches any character not enclosed. |
| **\[a-z\]** | A range of characters. Matches any character in the specified range. |
| **\[^a-z\]** | A negative range characters. Matches any character not in the specified range. |
| **b** | Matches a word boundary, that is, the position between a word and a space. |
| **B** | Matches a nonword boundary. ‘erB’ matches the ‘er’ in “verb” but not the ‘er’ in “never”. |
| **d** | Matches a digit character. |
| **D** | Matches a non-digit character. |
| **f** | Matches a form-feed character. |
| **n** | Matches a newline character. |
| **r** | Matches a carriage return character. |
| **s** | Matches any whitespace character including space, tab, form-feed, etc. |
| **S** | Matches any non-whitespace character. |
| **t** | Matches a tab character. |
| **v** | Matches a vertical tab character. |
| **w** | Matches any word character including underscore. |
| **W** | Matches any non-word character. |
| **un** | Matches n, where n is a Unicode character expressed as four hexadecimal digits. For example, u00A9 matches the copyright symbol |

Origin: http://www.hscripts.com/tutorials/regular-expression/metacharacter-list.php

Examples:

**the quick brown fox jumped over the lazy dog**

Some of the patterns that can be applied to this sentence are as follows:

| **Command** | **Usage** |
|:-:|:-:|
| a.. | matches azy |
| b.\|j. | matches both br and ju |
| ..$ | matches og |
| l.\* | matches lazy dog |
| l.\*y | matches lazy |
| the.\* | matches the whole sentence |