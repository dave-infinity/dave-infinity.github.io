---
id: 1004
title: 'Linux Ubuntu Kernel Management'
date: '2019-12-23T11:38:29+00:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1004'
permalink: /2019/12/linux-ubuntu-kernel-management/
categories:
    - Linux
tags:
    - kernel
---

To revert to the latest recommended kernel:

```
<pre class="wp-block-code">```
sudo apt-get install --install-recommends linux-generic-hwe-18.04
```
```

To maintain the kernel and cleanse the unused:

```
<pre class="wp-block-code">```
You should check partially removed kernels with

dpkg -l linux-image-\* | grep ^rc

and remove them with for example sudo apt-get purge linux-image-4.4.0-101-generic.

Purging will remove initramfs generation rules from /var/lib/initramfs-tools/.

If it does not help, you can remove them manually from initramfs list:

sudo rm /var/lib/initramfs-tools/3.13.0-39-generic
sudo rm /var/lib/initramfs-tools/4.4.0-101-generic
sudo rm /var/lib/initramfs-tools/4.4.0-103-generic
sudo rm /var/lib/initramfs-tools/4.4.0-38-generic
sudo rm /var/lib/initramfs-tools/4.4.0-45-generic
sudo rm /var/lib/initramfs-tools/4.4.0-59-generic
sudo rm /var/lib/initramfs-tools/4.4.0-77-generic
sudo rm /var/lib/initramfs-tools/4.4.0-78-generic
sudo rm /var/lib/initramfs-tools/4.4.0-81-generic

Usually I run purge-old-kernels followed by sudo apt-get autoremove to have only 2 recent kernels.

You can reinstall installed kernels with their initramfses:

sudo apt-get install --reinstall \
$(dpkg -l linux-image-\* | grep ^ii | awk '{print $2}')

```
```

ref: <https://askubuntu.com/questions/1001285/why-are-old-initrd-files-of-uninstalled-kernels-filling-up-boot-partition>