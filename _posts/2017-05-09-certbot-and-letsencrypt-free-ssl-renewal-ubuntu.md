---
id: 785
title: 'Certbot and letsEncrypt free SSL renewal Ubuntu'
date: '2017-05-09T15:08:35+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=785'
permalink: /2017/05/certbot-and-letsencrypt-free-ssl-renewal-ubuntu/
categories:
    - 'Web Design'
tags:
    - cert
    - certificates
    - letsencrypt
    - renewal
    - ssl
---

1. Enable TCP:443 access to the server from the internet
2. Check local IPTABLES fw access for public TCP:443 access too
3. SSH into the server and run the following command:  
    sudo certbot — –force-renewal -d &lt;certname here&gt;

ref: https://certbot.eff.org/docs/