---
title: Getting a VPN Router
layout: post
tags: vpn
---

A Router is a computer that has minimum of at least two network interface cards that supports the internet protocol. It decides on how to forward IP packets and connects the network to the internet and various networks. Software for router functions can be added to a server. Read more about VPN router.

The article covers:
    Router
    Various routing protocols
    VPN Router

## Router

A network communicates or sends information in the form of packets. Router is usually a device/computer with at least two network interface cards support the Internet protocol. It looks at the IP packets and decides how to forward it. Routers operate at the network layer of the OSI reference model and connect networks or connect the network to the internet. A router receives packets from an interface card and reads the address on the IP packet and forwards it to an appropriate output network interface. Before sending the packet the link protocol header is replaced by the router. The packets are forwarded depending on the packets IP destination address and routing information. A routing table specifies network IP addresses that are known with appropriate network interface to be used for a packet to reach the destination. In case of LAN's routers; they decide whether the packet is for a local computer or for the internet depending on the Address (IP Address or subnet address)

- Within a LAN network routers separate local area networks into sub networks and balance traffic between workgroups as well filter traffic for security purposes. Many times they are used at the edge of the network to connect to remote offices or to connect to an ISP.
- For Enterprise networks these serve as a connector of all internal networks via the Ethernet. These also connect to the outside network via T3, ATM, Cable modem or other links. There fore they act as a major switching point for all packets within the network as well as outside. 

Even if the network architecture (token ring or Ethernet) differs routers can connect them. However routers cannot transform information from one data format to another (TCP/IP to IPX/SPX). If the routing table does not indicate proper address of a packet then the packet is discarded. If a routers is configured manually and the information in the router table is fixed then it is called a static router. If the routing tables are automatically decided (routers exchange routing tables) depending on algorithms then it is a dynamic router. Distance Vector algorithm is based on hop count of satellites, and periodically broadcast routing tables to other routers. Link state algorithm is another algorithm with broadcast routing tables at only at the start up. Multi protocol routers support more than one protocol. The various routing protocols are

- IS-IS, -Intermediate system to intermediate system
- IPX - Internet Packet Exchange
- NLSP - Netware Link Services protocol
- RIP - Routing information protocol

Software for VPN router functions or normal router functions can be added to a server or a specialized computer is optimized for communication. Routers in older Novell terminology were called 'network layer bridges'; they are also called gateways. 
