---
id: 624
title: 'University Mailing Workaround for An Alias to Email more than 1 person'
date: '2016-04-21T11:54:31+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=624'
permalink: /2016/04/university-mailing-workaround-for-an-alias-to-email-more-than-1-person/
categories:
    - Email
tags:
    - alias
    - email
    - 'email alias'
    - 'mailing list'
---

A solution from a friend at St. John’s College:

morning think i got the setting for using a mail list to distribute an alias to multiple addresses. Set up mailing list with the email address of the people its to be distributed to.

Configure the mail list . In list config – Sending/recieving setup –  
Who can send messages from – Public list (public)  
the subject tagging – Web team is what i used, some text here is appended to the subject line making it easier to identify  
Require the list address to appear in To or CC fields – off

this allows anyone to post unmoderated, adds Web Team to the subject for identification and allows the alias address to post to the mailing list

On the Non personal email routing page  
Set the alias to forward to the mail list address

it kept failing and thing it was the bit Require the list address to appear in To or CC fields which is on by default and needs to be off as it is not actually going to the mailist address but the alias