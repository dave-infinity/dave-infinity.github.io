---
id: 179
title: 'Disable Spell checker'
date: '2014-06-13T14:18:23+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=179'
permalink: /2014/06/disable-spell-checker/
categories:
    - Microsoft
    - Uncategorized
tags:
    - 'disable spelling'
    - exam
    - examination
    - gpo
    - 'spell checker'
    - spelling
---

Needed this info to disable spell checker for exam pc’s.

Firstly use MS Office admx files to manage those GPO elements. Then disable everything in “Word Options &gt; Proofing” and “Word Options &gt; Proofing &gt; Autocorrect”.

Next locate “Administrative Templates &gt; MS Office Word 20XX &gt;Disable Items in User Interface” , then browse to “Custom” – then select “Disable Commands”

Choose “Enable” and add the following items:

```

15780
9056
6111
12842
14453
4025
3997
3958
790
2
3217
2349
329
3219
2469
2788
11323
7343
7387
```

Next select ‘Disable Shortcut Keys’ and enter the following values:

```

118 254 79,12 118,16 118,4

```

below are details of the command shortcuts:

```

Below details exactly what each value does:

Commands
2566 – Proofing
9056 – ThesaurusRR
6111 – Translation Pane
12842 – Translation Screen Tip
14453 – English Assistant
4025 – Translate to simplified Chinese
3997 – Translate to traditional Chinese
3958- TCSCTranslator
790 – Set Language
2 – Spelling
3217 – Hide spelling errors
2349 – Tools Spelling Recheck Document
329 – Grammar
3219 – Dictionary
2469 – Tools Grammar Settings
2788 – Tools Options Proofing
11323 – disables the ‘Options’ bar under the Office ‘flower’ button.
7343 – WPRefPane
7387 – Reading Mode Lookup
Shortcut Keys
118 – F7 – Shortcut for spellcheck
84,216 – Alt-T – Legacy Tools Menu
79,12 – Ctr+Shift+O – Opens the research bar
118,16 – Alt +F7
118,4 – Shift+F7

```