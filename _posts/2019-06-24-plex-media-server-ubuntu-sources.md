---
id: 923
title: 'Plex Media Server Ubuntu Sources'
date: '2019-06-24T22:10:45+01:00'
author: Dave
layout: post
guid: 'https://www.oxfordshirecomputing.co.uk/?p=923'
permalink: /2019/06/plex-media-server-ubuntu-sources/
categories:
    - Server
tags:
    - apt
    - media
    - plex
    - sources
---

## Thanks to https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/how-to-install-plex-media-server-on-ubuntu-18-04-ubuntu-16-04-linux-mint-19.html 

### Using Plex Repository

Import the Plex repository’s GPG key using the curl command.

```
<pre class="wp-block-preformatted">curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
```

Add the Plex repository to your system using the below command

```
<pre class="wp-block-preformatted">echo "deb https://downloads.plex.tv/repo/deb public main" | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
```

Now, update the apt index and install the latest version of the Plex Media Server.

```
<pre class="wp-block-preformatted">sudo apt update
sudo apt install -y plexmediaserver
```

Plex Media Server package places repository configuration in `/etc/apt/sources.list.d` directory. Since we already have the `plexmediaserver.list` in the repo directory, the installer may ask you below questions. Type **Y** and press enter.

```
<pre class="wp-block-preformatted">Configuration file '/etc/apt/sources.list.d/plexmediaserver.list'
 ==> File on system created by you or by a script.
 ==> File also in package provided by package maintainer.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** plexmediaserver.list (Y/I/N/O/D/Z) [default=N] ? Y
Installing new version of config file /etc/apt/sources.list.d/plexmediaserver.list ...
```