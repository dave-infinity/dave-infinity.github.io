---
id: 1045
title: 'RHEL Useful Commands'
date: '2020-11-05T12:11:15+00:00'
author: oxcompdave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=1045'
permalink: /2020/11/rhel-useful-commands/
categories:
    - Ukategorisert
---

The following are some basic command references

Systemctl

```
<pre class="wp-block-code">```
systemctl reload-or-restart <servicename>

systemctl list-unit-files --state=[enabled|disabled]

systemctl list-unit-files --type=[service|other]

systemctl list-dependencies <servicename>

systemctl [mask|unmask] <servicename>

systemctl enable [--now] <servicename>

systemctl disable [--now] <servicename>
```
```

Output redirection (bash)

```
<pre class="wp-block-code">```
#redirect stdout to overwrite a file	
command > file
#redirect stdout to append to a file	
command >> file
#redirect stderr to overwrite a file	
command 2> file
#discard stderr error messages by redirecting to /dev/null
command 2> /dev/null
#redirect stdout and stderr to overwrite the same file
command > file 2>&1
command &>file
#redirect stdout and stderr to append to the same file
command >> file  2>&1
command &>>file
```
```

Bash shell expansions

{item1,item2…} for each of the items in the list

$VARIABLE – include the value of the variable

$() command substitution, execute the command and use the STDOUT results within the current command  
e.g.: **`echo The day is $(date +%A).`**

<figure class="wp-block-table">| glob pattern | results |
|---|---|
| \* | zero or more characters. |
| ? | A single character |
| \[*`abc...`*\] | Any one character in the selection |
| \[!*`abc...`*\] | Any one character *not* in the selection |
| \[^*`abc...`*\] | Any one character *not* in the selection |
| \[\[:alpha:\]\] | Any single alphabetic character |
| \[\[:lower:\]\] | Any single lowercase character |
| \[\[:upper:\]\] | Any single uppercase character |
| \[\[:alnum:\]\] | Any single alphabetic character or digit |
| \[\[:punct:\]\] | Any single printable character not a space or alphanumeric |
| \[\[:digit:\]\] | Any single digit from 0 to 9. |
| \[\[:space:\]\] | Any single white space character |

</figure>SELinux

```
<pre class="wp-block-code">```
# list processes with SELinux contexts
ps axZ

#list files with SELinux contexts
ls -Z

# Manage system wide SELinux
/etc/selinux/config

getenforce

setenforce


# he kernel argument enforcing=0 boots the system into permissive mode; 
# enforcing=1 sets enforcing mode.
# Disable SELinux completely by passing on the kernel parameter 
# selinux=0 disables
# selinux=1 enables  

# change context temporarily:
chcon -t httpd_sys_content_t 

# restore default contexts recursively -R with verbose output -v:
restorecon -Rv [directory|file]

# Inspect contexts
semanage fcontext -l

# Apply new context permanently (all files and directories below /virtual):
semanage fcontext -a -t httpd_sys_content_t '/virtual(/.*)?'
restorecon -RFvv /virtual

# SELinux boolean controls
# list all current boolean settings:
getsebool -a

# switch a boolean on or off temporarily:
setsebool <boolean name> [on|off]

# switch a boolean on or off permanently:
setsebool -P <boolean name> [on|off]

# list boolean states running which differ from the default state :
semanage boolean -l -C

# Investigate SELinux events:
tail /var/log/audit/audit.log
# look for "type=AVC" or "avc:  denied" or "scontext="

tail /var/log/messages
# look for "SELinux is preventing" and within the log "sealert -l <identifier>"

# To gather more detailed information on the SELinux event, using the identifier in the messages log:
sealert -l <identifier>

# also you can search messages for SELinux via:
ausearch -m AVC -ts recent
```
```

Disk Management

```
<pre class="wp-block-code">```
# list all block devices
lsblk 

# list /dev/vda partition table
parted /dev/vda print

# first define the partition table type 
parted /dev/vda mklabel  [msdos|gpt]

# create a partition of type xfs from the start to 1GB in size
parted /dev/vda mkpart primary xfs 2048s 1000MB

# for swap for the next logical partition and 500MB in size:
mkfs.xfs /dev/vda mkpart <name> linux-swap 1001MB 1501MB
swapon /dev/vda2
swapon --show

# make it permanent
lsblk --fs /dev/vda2
UUID=cb7f71ca-ee82-430e-ad4b-7dda12632328  swap  swap  defaults  0 0

# format that parition with a filesystem
mkfs.xfs /dev/vda1


```
```