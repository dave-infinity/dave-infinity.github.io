---
id: 858
title: 'eSXi update storage drivers'
date: '2018-02-25T09:04:23+00:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=858'
permalink: /2018/02/esxi-update-storage-drivers/
categories:
    - Virtualization
tags:
    - driver
    - esxi
    - maintenance
    - mode
    - reboot
    - storage
    - vmware
---

1\. Power down all running VMs on host (or migrate to another eSXi host if using vCenter)

2\. Enable SSH on the eSXi host

3\. SSH to the host

4\. Enter maintenance mode via:

```
esxcli system maintenanceMode set --enable true
```

5\. Uninstall the previous storage driver via:

```
esxcli software vib remove -n scsi-hpvsa -f
```

6\. Reboot the eSXi host via:

```
esxcli system shutdown reboot --reason "<strong>your reason here" </strong>
```

7\. When the eSXi host is back SSH back in and ensure Maintenance Mode is enabled through the same command in step 4.

8\. SCP / SFTP copy the new storage driver to /tmp/ on the eSXi host

9\. Install the new storage drive via:

```
esxcli software vib install -v file:/tmp/<strong>name-of-driver-file-here.vib</strong> --force --no-sig-check --maintenance-mode
```

10\. Reboot

11\. Disable SSH

12\. Exit Maintenance Mode

13\. Power on / migrate back VMs