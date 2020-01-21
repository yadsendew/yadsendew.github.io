---
layout: post
title: Network Layer Part 1
date: 2020-01-19 09:12 +0000
publish: true
toc: true
categories: ["Computer Networks"]
---
# Network Layer
![](/assets/img/2020-01-20-19-48-26.png)
![](/assets/img/2020-01-20-20-21-14.png)
## Functions of the Network Layer
* Sender: Pack segments of the Transport Layer into pakets 
* Receiver: Identify the packets inside the frames of Data Link Layer
* Provide logical addresses (IP address) 
* Routing = Determinate the best path to the destination 
* Forward packets between logical networks (across diﬀerent physical networks)

Delivery of packets requires **IP addresses**, Network Layer specifies their format.  
The most commonly used Network Layer protocol is **Internet Protocol (IP)**  
## Devices of Network Layer: 
* **Router**: forward packets between networks with diﬀerent logical address ranges
    * Provide exactly like Hubs and Switches multiple interfaces 
    * Enable to connect the local network (LAN) with a WAN (e.g. via DSL or 3G/4G mobile network)
* **Layer-3-Switch** (Router without WAN port)  
* **Gateways** 
are protocol converters
  * Enable communication between networks, which base on diﬀerent protocols 
  * A Gateway can in theory operate on all layers 
  * Gateways, which operate at the Network Layer, are also called Multiprotocol Routers  

      **IP address of the Gateway = Default Gateway**. Today, **Default Gateway := Router address**, because a Gateway is usually not required any longer. Thus, the term _Default Router_ would be suited better
      **VPN-Gateways may operate on Network Layer**

## Collision Domain
Devices on **layer 1** do **not divide** the **collision domain** (Repeaters, Hubs)  
Devices on **layer 2 and 3** **divide the collision domain** (Bridges, Layer-2-Switches, Routers, Layer-3-Switches)  
## Broadcast Domain
Logical part of a network, a broadcast reaches all network devices belongs to that domain.  
Devices on **layer 3** **divide** broadcast domain  
Devices on **layer 1 & 2** do **not divide** broadcast domain  
**Broadcast domains** consist of one or more **collision domains**

Router: **each port** of a Router **connects diﬀerent IP**
## Addressing in the Network Layer
**Problem:** MAC addresses is not useful in large-scale computer networks  
**Solution**: Logical addresses is independent from the speciﬁc hardware    
**Logical addressing** separates the view of humans (logical addresses) from the internal view of computers and software (physical addresses)  


Every Network Layer **packet contains the receiver's IP address**  
An IP address :=
* single receiver - Unicast
* group of receivers - Multicast (Broadcast)

Multiple IP addresses := single network devices     
With Anycast, a **single receiver of a group** can be reached via a **single address**

## Format of IP Address
IPv4 addresses have a length of 32 bits => 2^32 addresses  

![](/assets/img/2020-01-21-12-09-11.png)
![](/assets/img/2020-01-21-12-10-04.png)
### Drawback: 