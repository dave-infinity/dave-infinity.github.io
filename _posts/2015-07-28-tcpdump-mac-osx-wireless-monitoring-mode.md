---
id: 506
title: 'tcpdump Mac OSX Wireless Monitoring Mode'
date: '2015-07-28T11:47:20+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=506'
permalink: /2015/07/tcpdump-mac-osx-wireless-monitoring-mode/
categories:
    - 'MAC OSX'
    - Networking
tags:
    - monitoring
    - networking
    - sniffing
    - tcpdump
    - wireless
---

### The preamble

Steve Kersley provided me with a quick tute in using the native Mac OSX tools to monitor the local wifi clients and access points.

### The prep

First prep the symlink on the machines

```
sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/sbin/airport
```

### The Commands

Next run the dissassociate command on the wireless adpater:

```
sudo airport -z
```

finally run the tcpdump command to begin monitoring the wireless activity in realtime

```
sudo tcpdump -i en1 -I -n type mgt and not subtype beacon
```

### The explanation

The previous command is broken down into:

- -i en1 : specify the interface to listen on
- -I : Print the interface on each dump line.
- -n : do not convert address (don’t use DNS resolution)
- type mgt and not subtype beacon : filter the packets by type mgt (exclude ctl and data) and also just examine the beacon data for dis/associate events

The above is fairly self-explanatory except for the last options for filtering by type.

An excellent resource I used for reference to understand this can be found at [http://www.wildpackets.com/resources/compendium/wireless\_lan/wlan\_packet\_types](http://www.wildpackets.com/resources/compendium/wireless_lan/wlan_packet_types)

and is included below for reference:

## 802.11 WLAN Packet Types

<a name="wp1002245"></a>

The table below lists the various packet types and subtypes specified in the 802.11 WLAN standard, and describes their usage briefly.

<a name="wp1002234"></a>

<div align="left"><a name="wp1004352"></a>Table E.1 WLAN packet types
| <a name="wp1001728"></a><div><div align="center">**Packet Types**</div></div> | <a name="wp1001736"></a><div><div align="center">**Usage**</div></div> |
|---|---|
| <a name="wp1001738"></a><div><div align="center">**type**</div></div> | <a name="wp1001742"></a><div><div align="center">**subtype**</div></div> | <a name="wp1001746"></a><div><div align="center"> </div></div> |
| <a name="wp1001758"></a>00 | <a name="wp1001760"></a>mgmt | <a name="wp1001762"></a>0000 | <a name="wp1001764"></a>Association Request | <a name="wp1001766"></a>This packet is sent to an access point (in a BSS or ESS) or to any other peer (in an IBSS or ad hoc network). The sender must already be authenticated in order to gain a successful association. |
| <a name="wp1001768"></a>00 | <a name="wp1001770"></a>mgmt | <a name="wp1001772"></a>0001 | <a name="wp1001774"></a>Association Response | <a name="wp1001776"></a>This packet is sent from an access point (in a BSS or ESS) or from any other peer (in an IBSS or ad hoc network) in response to an association request packet. If the request is successful, the response will include the Association ID of the requester. |
| <a name="wp1001778"></a>00 | <a name="wp1001780"></a>mgmt | <a name="wp1001782"></a>0010 | <a name="wp1001784"></a>Reassociation Request | <a name="wp1001786"></a>Like an association request, but it includes information about the current association at the same time as it requests a new association (either with the original Station after some lapse of time, or with a new station upon moving from one BSS to another). This packet is sent to an access point (in a BSS or ESS) or to any other peer (in an IBSS or ad hoc network). The sender must already be authenticated in order to gain a successful association. |
| <a name="wp1001788"></a>00 | <a name="wp1001790"></a>mgmt | <a name="wp1001792"></a>0011 | <a name="wp1001794"></a>Reassociation Response | <a name="wp1001796"></a>Like an association response, but in response to a reassociation request. This packet is sent from an access point (in a BSS or ESS) or from any other peer (in an IBSS or ad hoc network) in response to a reassociation request packet. If the request is successful, the response will include the Association ID of the requester. |
| <a name="wp1001798"></a>00 | <a name="wp1001800"></a>mgmt | <a name="wp1001802"></a>0100 | <a name="wp1001804"></a>Probe Request | <a name="wp1001806"></a>Probe request is used to actively seek any, or a particular, access point or BSS. |
| <a name="wp1001808"></a>00 | <a name="wp1001810"></a>mgmt | <a name="wp1001812"></a>0101 | <a name="wp1001814"></a>Probe Response | <a name="wp1001816"></a>Probe response replies with station parameters and supported data rates. |
| <a name="wp1001818"></a>00 | <a name="wp1001820"></a>mgmt | <a name="wp1001822"></a>1000 | <a name="wp1001824"></a>Beacon | <a name="wp1001826"></a>Beacon packets are sent by the access point in a BSS (or its equivalent in an IBSS) to announce the beginning of a Contention Free period (CF), during which the right to transmit is conferred by the access point by polling. <a name="wp1002249"></a><a name="wp1002250"></a>Beacon management packets carry BSS timestamps to help synchronize member stations with the BSS, and other information to help them locate and choose the BSS with the best signal and availability. |
| <a name="wp1001838"></a>00 | <a name="wp1001840"></a>mgmt | <a name="wp1001842"></a>1001 | <a name="wp1001844"></a>ATIM | <a name="wp1001846"></a>Announcement Traffic Indication Message. This packet serves much the same function in an IBSS that the Beacon packet does in an infrastructure (BSS or ESS) topology. The packet sets the synchronization of the group and announces that messages are waiting to be delivered. Stations in Power Save mode wake up periodically to listen for ATIM packets in ad hoc (IBSS) networks, just as they do for Beacon packets in infrastructure (BSS or ESS) networks. |
| <a name="wp1001848"></a>00 | <a name="wp1001850"></a>mgmt | <a name="wp1001852"></a>1010 | <a name="wp1001854"></a>Disassociation | <a name="wp1001856"></a>This packet is an announcement breaking an existing association. It is a one-way communication (meaning it does not require or accept a reply), and must be accepted. It can be sent by any associated station or BSS and it takes effect immediately. |
| <a name="wp1001858"></a>00 | <a name="wp1001860"></a>mgmt | <a name="wp1001862"></a>1011 | <a name="wp1001864"></a>Authentication | <a name="wp1001866"></a>Authentication packets are sent back and forth between the station requesting authentication and the station to which it is attempting to assert its authentic identity. The number of packets exchanged depends on the authentication method employed. Information relating to the particular scheme is carried in the body of the Authentication packet. |
| <a name="wp1001868"></a>00 | <a name="wp1001870"></a>mgmt | <a name="wp1001872"></a>1100 | <a name="wp1001874"></a>Deauthentication | <a name="wp1001876"></a>This packet is an announcement stating that the receiver is no longer authenticated. It is a one-way communication from the authenticating station (a BSS or functional equivalent), and must be accepted. It takes effect immediately. |
| <a name="wp1001888"></a>01 | <a name="wp1001890"></a>ctrl | <a name="wp1001892"></a>1010 | <a name="wp1001894"></a>PS-Poll | <a name="wp1001896"></a>Power Save polling packet. Stations in power save mode awaken periodically to listen to selected Beacons. If they hear that data is waiting for them, they will awake more fully and send a PS-Poll packet to the access point (BSS) to request the transmission of this waiting data. <a name="wp1002288"></a><a name="wp1002289"></a>In Control packets of the Power Save-Poll type, the Duration/ID field contains the association ID (AID) for the station sending the packet. |
| <a name="wp1001898"></a>01 | <a name="wp1001900"></a>ctrl | <a name="wp1001902"></a>1011 | <a name="wp1001904"></a>RTS | <a name="wp1001906"></a>Request To Send. Coordinates access to airwaves. |
| <a name="wp1001918"></a>01 | <a name="wp1001920"></a>ctrl | <a name="wp1001922"></a>1100 | <a name="wp1001924"></a>CTS | <a name="wp1001926"></a>Clear To Send. Response to a RTS, coordinates access to airwaves. |
| <a name="wp1001938"></a>01 | <a name="wp1001940"></a>ctrl | <a name="wp1001942"></a>1101 | <a name="wp1001944"></a>ACK | <a name="wp1001946"></a>Acknowledges receipt of transmitted data. |
| <a name="wp1001958"></a>01 | <a name="wp1001960"></a>ctrl | <a name="wp1001962"></a>1110 | <a name="wp1001964"></a>CF End | <a name="wp1001966"></a>Signals the end of Contention Free period. |
| <a name="wp1001968"></a>01 | <a name="wp1001970"></a>ctrl | <a name="wp1001972"></a>1111 | <a name="wp1001974"></a>CF End + CF ACK | <a name="wp1001976"></a>Signals the end of the Contention Free period and Acknowledges the receipt of some packet in a single message. |
| <a name="wp1001978"></a>10 | <a name="wp1001980"></a>data | <a name="wp1001982"></a>any | <a name="wp1001984"></a>any | <a name="wp1001986"></a>Multiple subtypes exist for Data type packets, but all have the same basic format, as described above. ([see Appendix C, “802.11 WLAN Packets and Protocols”](http://www.wildpackets.com/resources/compendium/manual_appendices/nxA1_AP#wp1001864).) <a name="wp1002227"></a><a name="wp1002212"></a>The different Data subtypes essentially just piggyback CF-Poll, CF-ACK, and CF-End messages onto the data message in a single transmission. This allows the BSS to gain higher throughputs possible using PCF (point coordinating function). |

</div>