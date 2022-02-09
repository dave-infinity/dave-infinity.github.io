---
id: 1028
title: 'iDrac 6, Linux, Firefox &#038; Natively Unsupported Virtual Console'
date: '2020-09-03T11:36:57+01:00'
author: Dave
layout: post
guid: 'http://www.oxfordshirecomputing.co.uk/?p=1028'
permalink: /2020/09/idrac-6-linux-firefox-natively-unsupported-virtual-console/
categories:
    - Dell
    - Linux
tags:
    - idrac
    - 'java re'
    - 'java security'
    - jnlp
---

So after a couple of hours toying and reading online (links to other pages which aided me in this assessment at the end of this post) I’d like to record the specific binaries and config changes I needed to make to access an elderly iDrac6 Virtual Console session from Firefox.  
  
My environment:  
Client:  
Fedora 32  
Firefox 80

Elderly Dell Server:  
iDrac 6  
Firmware 3.75 (Build 5)

1. Downloaded, verified &amp; installed the latest Oracle Java version in a .rpm format from   
    https://www.java.com/en/download/linux\_manual.jsp
2. Run the /usr/java/latest/bin/jcontrol to open the Oracle Java control panel.   
    Navigate to the “Security” tab, ensure “High” is the selected security level and then add your iDrac website address to the “Exception Site List” as shown in the example image below:

<figure class="wp-block-image size-large is-resized">![](https://www.oxfordshirecomputing.co.uk/wp-content/uploads/2020/09/image.png)<figcaption>Oracle Java Control Panel Site Exception Example</figcaption></figure>3\. Next, for my version of iDrac which uses the MD5 algorithm for security I needed to permit this, it is disabled by default in modern Java.  
Edit **/usr/java/jre1.8.0\_261-i586/lib/security/java.security** (your version may vary of course) and locate the following line, around about line number 612:

```
<pre class="wp-block-code">```
jdk.jar.disabledAlgorithms=MD2, MD5, RSA keySize < 1024, DSA keySize < 1024
```
```

4\. Copy and paste this line below itself, comment out the original and then edit the copy to read as follows (removing the MD5 entry)

```
<pre class="wp-block-code">```
jdk.jar.disabledAlgorithms=MD2, RSA keySize < 1024, DSA keySize < 1024
```
```

5\. That’s it, now visit the iDrac web interface, download the .jnlp file and run it with the following command:

```
<pre class="wp-block-code">```
javaws /path/to/the/downloaded/filename.jnlp
```
```

Do remember to restore the commented line and comment the edited line in your **/usr/java/jre1.8.0\_261-i586/lib/security/java.security** file after use – not good to leave insecure algorithms available to a commonly exploited platform!

References:  
<https://velenux.wordpress.com/2017/06/07/workaround-for-javaws-jnpl-error-cannot-grant-permissions-to-unsigned-jars/>

<https://unix.stackexchange.com/questions/143805/running-unsigned-javaws-code>