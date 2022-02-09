---
id: 1012
title: 'RHEL Subscription Manager Useful Commands'
date: '2020-03-27T15:48:12+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1012'
permalink: /2020/03/rhel-subscription-manager-useful-commands/
categories:
    - Linux
tags:
    - manager
    - rhel
    - subscription
    - subscription-manager
---

The following was copied from &lt;https://access.redhat.com/discussions/3312101?tour=8&gt; and provides a method of cleaning all subscription manager configuration and re-subscribing – you’ll need an active account with Red Hat to complete this though they do offer free developer accounts (use your account name and not your email address as the username!)

```
<pre class="wp-block-code">```
sudo subscription-manager remove --all
sudo subscription-manager unregister
sudo subscription-manager clean

sudo subscription-manager register
sudo subscription-manager refresh
sudo subscription-manager attach --auto
```
```