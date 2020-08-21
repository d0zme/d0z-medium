---
title: What is Port 7 on my network?
layout: post
permalink: /port-7
---

If you see port 7 being utilized on your network, it's likely to be: **Echo (tcp,udp) or WOL (Wake on LAN) (udp)**

## A little about Wake on Lan (WOL)

Many users have heard of Wake-On-LAN or WOL by its acronym, but have never quite understood the concept or do not know very well how to implement it. The simple possibility of turning on your computer from anywhere without physically "pressing" the power button is something we cannot take lightly. Therefore, we are going to see everything about Wake-On-LAN (WOL), concept, compatible network cards and how to activate it to work in Windows 10.

Our colleagues at RedesZone offer us a great manual on Wake-On-LAN (WOL), the function that allows us to remotely turn on the computer from anywhere in the world. But, first of all, let's briefly review the concept and see some previous considerations about it.
What is Wake-On-LAN (WOL)?

Wake-on-LAN is a network standard that allows you to turn on your computer remotely. It has a supplementary standard called Wake-on-Wireless-LAN (WoWLAN) for wireless networks. For WOL, we need our computer to have a number of components so that the function can be activated:

- Computer connected to the power grid
- ATX-compatible motherboard
- Network card with WOL enabled (depending on the manufacturer, enable Power on remote PCI, Wake on LAN or PME WakeUp events in the BIOS)

As this standard is widespread, it should work perfectly in all operating systems as long as we have compatible hardware. From the point of view of Windows 10 users, we will be able to use Wake-On-LAN (WOL) to turn on the computer or activate it from full off mode, hibernation or sleep.

### How does Wake-On-LAN (WOL) work?

The Wake-On-LAN (WOL) function is supported by the use of "magic packages". Basically, when the network card receives that "magic packet", it "tells" the computer to turn on. Therefore, the network card will always remain on with minimal power consumption to see if it detects that packet at any time.

But this packet is not just a packet. The "magic packet" contains the MAC address of the target computer, a numerical identifier that each network card or other network device has in the computer. In this way, it is possible to be recognized within the network.

The "magic packet" is a broadcast frame that contains a string of 6 bytes of value 255 ("FF FF FF FF" in hexadecimal), followed by 16 repetitions of the MAC address of the target computer. As mentioned above, this works if the network card and motherboard support the Wake-On-LAN (WOL) standard (Wikipedia Information).
