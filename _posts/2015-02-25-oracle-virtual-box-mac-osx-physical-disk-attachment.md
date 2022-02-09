---
id: 371
title: 'Oracle Virtual Box Mac OSX Physical Disk Attachment'
date: '2015-02-25T11:28:03+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=371'
permalink: /2015/02/oracle-virtual-box-mac-osx-physical-disk-attachment/
categories:
    - Hardware
    - 'MAC OSX'
tags:
    - osx
    - passthrough
    - 'physical disk'
    - virtualbox
    - writethrough
---

1\. Get the identity of the physical disk using  
“diskutil list”  
from the command line. Usually it’s named “System” if booting from an OSX Live USB drive

2\. Unmount the physical disk from the system

3\. From terminal create a holding VMDK file for Virtualbox to communicate with the physical disk through by:  
“sudo VBoxManage internalcommands createrawvmdk -filename &lt;&lt;DIR/FILE.vmdk&gt;&gt; -rawdisk /dev/disk&lt;&lt;#&gt;&gt;”

4\. Correct permissions on both the physical disk and the file you created, something like:  
“sudo chmod 777 /dev/disk&lt;&lt;#&gt;&gt;”  
and  
“sudo chown &lt;&lt;group&gt;&gt;:&lt;&lt;user&gt;&gt; &lt;&lt;DIR/FILE.vmdk&gt;&gt;”  
“sudo chmod 770 &lt;&lt;DIR/FILE.vmdk&gt;&gt;”

5\. Launch Virtualbox, create a new DOS VM and attach a SATA Controller and then the new VMDKfile as a SATA disk

6\. From Virtualbox “File&gt;Virtual Media Manager”, modify the &lt;&lt;DIR/FILE.vmdk&gt;&gt; so that it’s set as a “writethrough” disk

7\. Then attach the desired boot cd to the VM and ensure the boot order is correct

8\. Start the VM!