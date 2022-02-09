---
id: 107
title: 'Linux Test Bandwidth Between Two Servers'
date: '2014-01-29T10:00:37+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=107'
permalink: /2014/01/linux-test-bandwidth-between-two-servers/
categories:
    - Linux
    - Networking
tags:
    - linux
    - network
    - speed
    - testing
---

**RIPPED DIRECTLY FROM:** [http://linuxaria.com/article/tool-command-line-bandwidth-linux](http://linuxaria.com/article/tool-command-line-bandwidth-linux "http://linuxaria.com/article/tool-command-line-bandwidth-linux")

\[expand title=”**3 Command line tools to test bandwidth between 2 servers** “\]

One element that is often not know, or that should be measured after a problem statement or after a change in the infrastructure is the [network](http://linuxaria.com/tag/network "network") . But how do you accurately measure the speed between two servers?

Someone use ftp, scp or other file transfer protocols, these can give some indication, but probably you’ll measure the limit of your disks or CPU.

In this article I will show you 3 way to measure the [bandwidth](http://linuxaria.com/article/tool-command-line-bandwidth-linux "bandwidth") from the command line, without using the disks.

### [Iperf](http://iperf.sourceforge.net/)

Iperf was developed by NLANR/DAST as a modern alternative for measuring maximum TCP and UDP bandwidth performance. Iperf allows the tuning of various parameters and UDP characteristics. Iperf reports bandwidth, delay jitter, datagram loss.

The quality of a link can be tested as follows:  
– Latency (response time or RTT): can be measured with the Ping command.  
– Jitter (latency variation): can be measured with an Iperf UDP test.  
– Datagram loss: can be measured with an Iperf UDP test.

The bandwidth is measured through TCP tests.

To be clear, the difference between TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) is that TCP use processes to check that the packets are correctly sent to the receiver whereas with UDP the packets are sent without any checks but with the advantage of being quicker than TCP.  
Iperf uses the different capacities of TCP and UDP to provide statistics about network links.

With Iperf you have a server machine where iperf put itself in listening and the other that is the client that send the informations.

Example:

[![Iperf-example](http://www.monkeyandlamb.co.uk/itblog/wp-content/uploads/2014/01/Iperf-example-300x112.gif)](http://www.monkeyandlamb.co.uk/itblog/wp-content/uploads/2014/01/Iperf-example.gif)

Basic usage:

**Server side:**

<div>| ``` #iperf -s ------------------------------------------------------------ Server listening on TCP port 5001 TCP window size: 8.00 KByte (default) ------------------------------------------------------------ [852] local 10.1.1.1 port 5001 connected with 10.6.2.5 port 54355 [ ID]   Interval          Transfer        Bandwidth [852]   0.0-10.1 sec   1.15 MBytes   956 Kbits/sec ------------------------------------------------------------ Client connecting to 10.6.2.5, TCP port 5001 TCP window size: 8.00 KByte (default) ------------------------------------------------------------ [824] local 10.1.1.1 port 1646 connected with 10.6.2.5 port 5001 [ ID]   Interval          Transfer        Bandwidth [824]   0.0-10.0 sec   73.3 MBytes   61.4 Mbits/sec ``` |
|---|

</div>**Client side**

<div>| ``` #iperf -c 10.1.1.1 -d ------------------------------------------------------------ Server listening on TCP port 5001 TCP window size: 85.3 KByte (default) ------------------------------------------------------------ ------------------------------------------------------------ Client connecting to 10.1.1.1, TCP port 5001 TCP window size: 16.0 KByte (default) ------------------------------------------------------------ [ 5] local 10.6.2.5 port 60270 connected with 10.1.1.1 port 5001 [ 4] local 10.6.2.5 port 5001 connected with 10.1.1.1 port 2643 [ 4] 0.0-10.0 sec 76.3 MBytes 63.9 Mbits/sec [ 5] 0.0-10.1 sec 1.55 MBytes 1.29 Mbits/sec ``` |
|---|

</div>So using Iperf (with appropriate flags) on both our machines we can simply measure the bandwidth between them.

Iperf is available also for Windows.

Complete guide: http://openmaniak.com/iperf.php

<iframe allowfullscreen="" frameborder="0" height="360" loading="lazy" src="//www.youtube.com/embed/H_dvLKGue90?feature=player_embedded" width="640"></iframe>

### Netcat

To eliminate the disks from having any part of the transfer, we will use netcat transferring the output of command yes. Netcat is described as being a “feature-rich network debugging and exploration tool”. It can be obtained from Source Forge, or it may already be available in your distribution.

Again we will use one of the machines as a server that receives the data and the other as a client that sends the information.

Basic usage  
On th server machine

<div>| ``` nc -v -v -l -n  2222 &gt;/dev/null listening on [any] 2222 ... ``` |
|---|

</div>On the client machine

<div>| ``` time yes\|nc -v -v -n 10.1.1.1 2222 &gt;/dev/null ``` |
|---|

</div>On client stop the process after 10 seconds (more or less) with ctrl-c, you’ll get something like:

<div>| ``` sent 87478272, rcvd 0  real 0m9.993s user 0m2.075s sys 0m0.939s ``` |
|---|

</div>On the server machine, note the data received (in bytes)

<div>| ```  sent 0, rcvd 87478392 ``` |
|---|

</div>Now multiply the bytes rcvd by 8 to get total bits, then divide by the time: Result in this example is 70Mb/s

Reference: http://deice.daug.net/netcat\_speed.html

### [Bandwidth Test Controller (BWCTL)](http://www.internet2.edu/performance/bwctl/)

BWCTL is a command line client application and a scheduling and policy daemon. These tests can measure maximum TCP bandwidth, with various tuning options available, or, by doing a UDP test, the delay, jitter, and datagram loss of a network.

The bwctl client application works by contacting a bwctld process on the two test endpoint systems. BWCTL will work as a 3-party application. The client can arrange a test between two servers on two different systems. If the local system is intended to be one of the endpoints of the test, bwctl will detect whether a local bwctld is running and will handle the required server functionality if needed.

The bwctl client is used to request the type of throughput test wanted. Furthermore, it requests when the test should be executed. bwctld either responds with a tentative reservation or a test denied message. Once bwctl is able to get a matching reservation from both bwctld processes (one for each host involved in the test), it confirms the reservation. Then, the bwctld processes run the test and return the results. The results are returned to the client from both sides of the test. Additionally, the bwctld processes share the results from their respective sides of the test with each other.

[![bwctl-example](http://www.monkeyandlamb.co.uk/itblog/wp-content/uploads/2014/01/bwctl-example-300x245.png)](http://www.monkeyandlamb.co.uk/itblog/wp-content/uploads/2014/01/bwctl-example.png)

For more information check the man page: http://www.internet2.edu/performance/bwctl/manpages.html\[/expand\]