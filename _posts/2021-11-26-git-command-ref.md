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
# rebase $branchname to the master branch interactively (-i) to allow edits
git rebase master -i  $branchname 

git rebase -i HEAD~

# rebase the current branch to itself using the $num index of commits
# e.g. if a branch has had 2 commits and you want to squash them into 1 then $num=1
git rebase -i HEAD~$num

# forcibly (destructively if uncommitted changes) restore to last commit
git reset --hard origin/master
