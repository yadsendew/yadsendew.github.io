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
[Classes of IPv4 & Their structure](/assets/img/2020-01-21-12-09-11.png)  
[Prefix of classes](/assets/img/2020-01-21-12-10-04.png)
### Drawback: 
* It is impossible to dynamically adjust them 
* Many addresses are wasted  

`Solution: Logical networks are divided into SUBNET`

## Subnet Mask
For creating subnets, a subnet mask is required
* All hosts in a network have a subnet mask assigned
  * Length: 32 bits (4 bytes) 
  * It is used to specify the number of subnets and hosts
* Subnet mask **splits** the _host ID of an IP address_ into **subnet ID** and **host ID**
    * The **network ID** remains **unchanged**
    * The network mask **adds** another **level** **of hierarchy** into the IP address
![From](/assets/img/2020-01-21-12-32-56.png) ![To](/assets/img/2020-01-21-12-33-31.png)
* Structure of the subnet mask:
    * 1-bits indicate, which part of the address space is used for subnet IDs 
    * 0-bits indicate, which part of the address space is used for host IDs
    ![](/assets/img/2020-01-21-12-35-45.png)
### Calculation example for subnetting with IPv4
Consider IP address: `172.21.240.90/27`.  
The `27` behind the `/` is **number of 1-bits in the subnet mask**.   
`Subnet_Address = IP_Address AND Subnet_Mask`  
`Host_ID = IP_Address AND (NOT Subnet_Mask)`

### Private Network
`10.0.0.0/8`  
`172.16.0.0/12`  
`192.168.0.0/16`  
Private network address space are not allow to interfere with global internet => they are not routed in the Internet.
## Structure of IPv4 packets
This Network Layer transfer the IPv4 packets.  
[Structure of IPv4](/assets/pdf/IPv4 Structure.pdf)  
![](/assets/img/2020-02-01-13-57-05.png)  

* Version: 4 bits
* IHL: 4 bits
* Differentiated services: 8 bits
* Total length (16 bits)
* Identification (16 bits)
* Flags (3 bits)
* Fragment Offset (13 bits)
* Time To Live (8 bits)
* Protokoll ID (8 bits)
* Header checksum (16 bits)
* IP address (sender) (32 bits)
*  IP address (destination) (32bits)
*  Options / Padding can contain additional information such as a time stamp, this last field before the payload area is filled with padding bits (0 bits) if necessary, to ensure that the header size is an integer number of 32 bit words
*  Payload: data from the transport layer

## Packet fragmentation
* Mỗi packet có kích thước khác nhau và chúng lại khá lớn. Mà **phương tiện truyền dẫn** thì có những hạn chế của nó: không đủ khả năng để truyền một packet trong một lần, mà phải tách nhỏ ra để truyền.  
* Việc tách ra (và ghép lại) của một IP packets thành các packet nhỏ hơn (fragments) được gọi là **Packet fragmentation**.   
* The **Maximum Transmission Unit** (MTU) speciﬁes the **maximum payload of a frame** = **maximum size** of **an IP packet**. [Details](/assets/img/Details.png)  
* IP packets contain **a ﬂag** which can be **used to prohibit fragmentation**
  * If a Router needs to fragment but the fragmentation is prohibitedt, the Router discards.
* If network device does **not receive all fragments of an IP packet within** a certain **period of time** => **discards all received fragments**  

[Packet fragmentation example](assets/pdf/Packet Fragmentation Example.pdf)

## [IPv6](assets/pdf/IPv6.pdf)
