---
id: 252
title: 'Night Porter Email (Pyinstaller, PiP etc)'
date: '2014-07-21T10:58:46+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=252'
permalink: /2014/07/night-porter-email-pyinstaller-pip-etc/
categories:
    - Uncategorized
tags:
    - email
    - 'night porter'
    - pip
    - pyinstaller
    - python
    - windows
---

1\. Install Python 2.7

2\. Install PIP (from http://stackoverflow.com/questions/4750806/how-to-install-pip-on-windows)  
Python 2.x and Python ≤ 3.3

Flying in the face of its ‘batteries included’ motto, Python ships without a package manager. To make matters worse, Pip was–until recently–ironically difficult to install.

Official instructions

Per http://www.pip-installer.org/en/latest/installing.html

Download get-pip.py, being careful to save it as a .py file rather than .txt. Then, run it from the command prompt.

python get-pip.py  
You possibly need an administrator command prompt to do this. Follow http://technet.microsoft.com/en-us/library/cc947813(v=ws.10).aspx

Alternative instructions

The official documentation tells users to install Pip and each its dependencies from source. That’s tedious for the experienced, and prohibitively difficult for newbies.

For our sake, Christoph Gohlke prepares Windows installers (.msi) for popular Python packages. He builds installers for all Python versions, both 32 and 64 bit. You need to

Install setuptools http://www.lfd.uci.edu/~gohlke/pythonlibs/#setuptools  
Install pip http://www.lfd.uci.edu/~gohlke/pythonlibs/#pip  
For me, this installed Pip at C:Python27Scriptspip.exe. Find pip.exe on your computer, then add its folder (eg. C:Python27Scripts) to your path (Start / Edit environment variables). Now you should be able to run pip from the command line. Try installing a package:

pip install httpie  
There you go (hopefully)! Solutions for common problems are given below:

Proxy problems

If you work in an office, you might be behind a HTTP proxy. If so, set the environment variables http\_proxy and https\_proxy. Most Python applications (and other free software) respect these. Example syntax:

http://proxy\_url:port  
http://username:password@proxy\_url:port  
If you’re really unlucky, your proxy might be a Microsoft NTLM proxy. Free software can’t cope. The only solution is to install a free software friendly proxy that forwards to the nasty proxy. http://cntlm.sourceforge.net/

Unable to find vcvarsall.bat

Python modules can be part written in C or C++. Pip tries to compile from source. If you don’t have a C/C++ compiler installed and configured, you’ll see this cryptic error message.

Error: Unable to find vcvarsall.bat

You can fix that by installing a C++ compiler such as MinGW or Visual C++, but again it’s often easier to check Christoph’s site for your package http://www.lfd.uci.edu/~gohlke/pythonlibs/

3\. Install Pyinstaller  
http://pythonhosted.org/PyInstaller/#installing-using-pip

4\. Apply updated to porters.py via BitBucket

5\. Using updated porters.py run  
pyinstaller –onefile –noconsole –icon=portericon.ico porters.py