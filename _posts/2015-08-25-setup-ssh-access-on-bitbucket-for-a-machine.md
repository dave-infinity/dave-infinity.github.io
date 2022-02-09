---
id: 512
title: 'Setup SSH access on bitbucket for a machine'
date: '2015-08-25T14:44:02+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=512'
permalink: /2015/08/setup-ssh-access-on-bitbucket-for-a-machine/
categories:
    - git
tags:
    - bitbucket
    - git
    - 'ssh keys'
---

<https://confluence.atlassian.com/bitbucket/set-up-git-and-mercurial-ubuntu-linux-269982882.html>

## Step 1. Install Git

Ubuntu uses the apt package management system, which provides the command line utility apt-get and optional graphical interfaces, such as Synaptic and Aptitude. We’ll use apt-get to install packages, but if you’re more comfortable with GUIs, those options are available. Open a terminal window on your local system and do the following:

1. Enter the following command to install Git: <div class="panel"><div class="panelContent">`$ sudo apt-get install git`</div></div>
2. Verify the installation was successful by typing `which git` at the command line. <div class="panel"><div class="panelContent">`$ which git<br></br>/opt/local/bin/git`</div></div>
3. Configure your username using the following command. <div class="panel"><div class="panelContent">`$ git config --global user.name "Emma Paris"`</div></div>
4. Configure your email address using the following command. <div class="panel"><div class="panelContent">`$ git config --global user.email "eparis@atlassian.com"`</div></div><div class="panelContent"></div>

## Step 2. Ensure you have an SSH client installed

SSH is most likely included with your version of Mac OS or Linux. To make sure, do the following to verify your installation:

1. From your terminal window, enter the following command, which identifies the version of SSH you have installed.  
    If SSH is installed, you see something similar to the following: <div class="panel panel-default"><div class="panel-body">`$ ssh -v<br></br>OpenSSH_5.6p1, OpenSSL 0.9.8r 8 Feb 2011<br></br>usage: ssh [-1246AaCfgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec]<br></br>[-D [bind_address:]port] [-e escape_char] [-F configfile]<br></br>[-I pkcs11] [-i identity_file]<br></br>[-L [bind_address:]port:host:hostport]<br></br>[-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]<br></br>[-R [bind_address:]port:host:hostport] [-S ctl_path]<br></br>[-W host:port] [-w local_tun[:remote_tun]]<br></br>[user@]hostname [command]>`</div></div>If you have `ssh` installed, the terminal returns version information.  
    If you don’t have `ssh` installed, install it now.
2. List the contents of your `~/.ssh` directory.  
    If you don’t have an `.ssh` directory, don’t worry, you’ll create it the next section. If you have a `.ssh` directory or you may see something like this: <div class="panel panel-default"><div class="panel-body">`$ ls -a ~/.ssh<br></br>known_hosts`</div></div>If you have defined a default identity, you’ll see the two `id_*` files:
    
    <div class="panel panel-default"><div class="panel-body">`$ ls -a ~/.ssh<br></br>.        ..        id_rsa        id_rsa.pub    known_hosts`</div></div>In this case, the default identity used RSA encryption (`id_rsa.pub`). If you want to use an existing default identity for your Bitbucket account, skip the next section and go to [start the ssh-agent and load your keys](https://confluence.atlassian.com/bitbucket/set-up-ssh-for-git-728138079.html#SetupSSHforGit-startagent).

## Step 3. Set up your default identity

By default, the system adds keys for all identities to the `/Users/<yourname>/.ssh` directory on Mac OSX, or `/home/<yourname>/.ssh` on Linux. This procedure creates a default identity. If you have a default identity and you want to use it for Bitbucket, skip this step and go to [start the ssh-agent and load your keys](https://confluence.atlassian.com/bitbucket/set-up-ssh-for-git-728138079.html#SetupSSHforGit-startagent). If you have an existing default identity but you forgot the passphrase, you can also use this procedure to overwrite your default identity and create a fresh one.

<div class="panel panel-default"><div class="panel-wrapper"><div class="panel-heading">**Want to Use Multiple Identities?**</div><div class="panel-body">You can create multiple SSH identities. Doing this is an advanced topic and beyond the scope of this tutorial. For information on how to create multiple identities, see [Configure multiple SSH identities for GitBash, Mac OSX, &amp; Linux](https://confluence.atlassian.com/bitbucket/configure-multiple-ssh-identities-for-gitbash-mac-osx-linux-271943168.html).

</div></div></div>Use the following procedure to create a new default identity.

1. Open a terminal in your local system.
2. Enter `ssh-keygen` at the command line.  
    The command prompts you for a file where you want to save the key. If the `.ssh` directory doesn’t exist, the system creates one for you. <div class="panel panel-default"><div class="panel-body">`$ ssh-keygen<br></br>Generating public/private rsa key pair.<br></br>Enter file in which to save the key (/Users/emmap1/.ssh/id_rsa):`</div></div>
3. Press the Enter or Return key to accept the default location.
4. Enter and re-enter a passphrase when prompted.  
    Unless you need a key for a process such as script, you should always provide a passphrase. The command creates your default identity with its public and private keys. The whole interaction will look similar to the following: <div class="panel panel-default"><div class="panel-body">`$ ssh-keygen<br></br>Generating public/private rsa key pair.<br></br>Enter file in which to save the key (/Users/emmap1/.ssh/id_rsa):<br></br>Created directory '/Users/emmap1/.ssh'.<br></br>Enter passphrase (empty for no passphrase):<br></br>Enter same passphrase again:<br></br>Your identification has been saved in /Users/emmap1/.ssh/id_rsa.<br></br>Your public key has been saved in /Users/emmap1/.ssh/id_rsa.pub.<br></br>The key fingerprint is:<br></br>4c:80:61:2c:00:3f:9d:dc:08:41:2e:c0:cf:b9:17:69 emmap1@myhost.local<br></br>The key's randomart image is:<br></br>+--[ RSA 2048]----+<br></br>|*o+ooo.          |<br></br>|.+.=o+ .         |<br></br>|. *.* o .        |<br></br>| . = E o         |<br></br>|    o . S        |<br></br>|   . .           |<br></br>|     .           |<br></br>|                 |<br></br>|                 |<br></br>+-----------------+`</div></div>
5. List the contents of `~/.ssh` to view the key files. <div class="panel panel-default"><div class="panel-body">`$ ls -a ~/.ssh`</div></div>

## <span class="confluence-anchor-link" id="SetupSSHforGit-startagent"></span>Step 4. Start the ssh-agent and load your keys

If you are running OSX 10.6.8 or later you can skip this step. The OSX 10.6.8 system asks for your connection parameters the first time you try to establish a SSH connection. Then, it automatically starts the `ssh-agent` for you. If you don’t have OSX 10.6.8 or are running another Linux operating system, do the following:

1. Open a terminal window and enter the `ps -e | grep [s]sh-agent `command to see if the agent is running. <div class="panel panel-default"><div class="panel-body">`$ ps -e | grep [s]sh-agent<br></br>9060 ?? 0:00.28 /usr/bin/ssh-agent -l`</div></div>
2. If the agent isn’t running, start it manually with the following command: <div class="panel panel-default"><div class="panel-body">`$ ssh-agent /bin/bash`</div></div>
3. Load your new identity into the `ssh-agent` management program using the `ssh-add` command. <div class="panel panel-default"><div class="panel-body">`$ ssh-add ~/.ssh/id_rsa<br></br>Enter passphrase for /Users/emmap1/.ssh/id_rsa:<br></br>Identity added: /Users/emmap1/.ssh/id_rsa (/Users/emmpa1/.ssh/id_rsa)`</div></div>
4. Use the `ssh-add` command to list the keys that the agent is managing. <div class="panel panel-default"><div class="panel-body">`$ ssh-add -l<br></br>2048 7a:9c:b2:9c:8e:4e:f4:af:de:70:77:b9:52:fd:44:97 /Users/manthony/.ssh/id_rsa (RSA)`</div></div>

## Step 5. Install the public key on your Bitbucket account

1. From Bitbucket, choose ***avatar* &gt; Manage account** from the application menu.  
    The system displays the **Account settings** page.
2. Click **SSH keys**.  
    The **SSH Keys** page displays. If you have any existing keys, those appear on this page.
3. Back in your terminal window, copy the contents of your public key file.  
    For example, in Linux you can `cat` the contents. <div class="panel"><div class="panelContent">`$ cat ~/.ssh/id_rsa.pub`</div></div>In Mac OSX, the following command copies the output to the clipboard:
    
    <div class="panel"><div class="panelContent">`$ pbcopy < ~/.ssh/id_rsa.pub`</div></div>
4. Back in your browser, enter a **Label** for your new key, for example, `Default public key`.
5. Paste the copied public key into the SSH **Key** field: