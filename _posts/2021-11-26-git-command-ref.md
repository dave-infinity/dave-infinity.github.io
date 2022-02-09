---
id: 1085
title: 'Git Command Ref'
date: '2021-11-26T10:22:15+00:00'
author: oxcompdave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1085'
permalink: /2021/11/git-command-ref/
categories:
    - git
---

git rebase master -i HEAD~ # rebase to the tip of the master branch interactively, usually called from a branch

git rebase -i HEAD~

git rebase -i HEAD~$num #commit number to $num
