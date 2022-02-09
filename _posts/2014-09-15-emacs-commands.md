---
id: 271
title: 'emacs commands'
date: '2014-09-15T08:21:34+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=271'
permalink: /2014/09/emacs-commands/
categories:
    - Linux
tags:
    - 'emacs. linux'
---

Linux Foundation

**Working with emacs**

| **Key** | **Usage** |
|---|---|
| emacs myfile | Start emacs and edit myfile |
| **Ctrl-x i** | Insert prompted for file at current position |
| **Ctrl-x s** | Write to the file keeping current name |
| **Ctrl-x Ctrl-w** | Write to the file giving a new name when prompted |
| **Ctrl-x Ctrl-s** | Write to all files currently being worked on and exit |
| **Ctrl-x Ctrl-c** | Exit after being prompted if there any unwritten modified files |

**Changing Cursor Positions**

| **Key** | **Usage** |
|---|---|
| **arrow keys** | Use the arrow keys for up, down, left and right |
| **Ctrl-n** | one line down |
| **Ctrl-p** | one line up |
| **Ctrl-f** | one character left |
| **Ctrl-b** | one character right |
| **Ctrl-a** | move to beginning of line |
| **Ctrl-e** | move to end of line |
| **E-f** | move to beginning of next word |
| **E-b** | move back to beginning of preceding word |
| **E-&lt;** | move to beginning of file |
| **E-x** | goto-line n move to line n |
| **E-&gt;** | move to end of file |
| **Ctrl-v or Page Down** | move forward one page |
| **E-v or Page Up** | move backward one page |
| **Ctrl-l** | refresh and center screen |

**Searching for Text**

| **Key** | **Usage** |
|---|---|
| **Ctrl-s** | search forward for prompted for pattern, or for next pattern |

| **Ctrl-r** | search backwards for prompted for pattern, or for next pattern |
|---|---|

**Working with Text**

| **Key** | **Usage** |
|---|---|
| **Ctrl-o** | Insert a blank line. |
| **Ctrl-d** | Delete character at current position. |
| **Ctrl-k** | Delete the rest of the current line. |
| **Ctrl-\_** | Undo the previous operation. |
| **Ctrl- space** | Mark the beginning of the selected region. The end will be at the cursor position. |
| **Ctrl-w** | Delete the current marked text and write it to the buffer. |
| **Ctrl-y** | Insert at current cursor location whatever was most recently deleted |