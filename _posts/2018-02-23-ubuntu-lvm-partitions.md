---
id: 851
title: 'Ubuntu, LVM, Partitions'
date: '2018-02-23T07:32:47+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=851'
permalink: /2018/02/ubuntu-lvm-partitions/
categories:
    - Linux
tags:
    - disk
    - extend
    - 'logical volume'
    - lvm
    - partition
    - ubuntu
---

Ubuntu disk partition extension under LVM:

1/ extend the LVM volume (cheated with gparted but parted would work fine, this is the container partition for the “Volume Group”.

2/ Next launch LVM and use “lvdisplay” to print the current output, mine was a container group with a single logical volume named “root”

3/ Now I know the location and name of the LV I can issue the following command to expand it into the available free space created in step 1:

lvextend -l +100%FREE /dev/Container1/root

4/ Finally exit lvm and expand the file system to fill the LV:

sudo resize2fs /dev/Container1/root