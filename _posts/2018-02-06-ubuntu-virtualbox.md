---
id: 828
title: 'Ubuntu &#038; Virtualbox'
date: '2018-02-06T18:04:18+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=828'
permalink: /2018/02/ubuntu-virtualbox/
categories:
    - Linux
tags:
    - kernel
    - linux
    - module
    - ubuntu
    - virtualbox
---

Ubuntu 16.04 (kernel 4.14), Virtualbox

I was trying to install Oracle VirtualBox either from their repo or from the Ubuntu repo but both failed to compile the Kernel Module.

I tried various guides before actually reading the error log whereupon I found the “libelf-dev” package was required (at least for installing virtualbox-5.2 from Oracle directly!).