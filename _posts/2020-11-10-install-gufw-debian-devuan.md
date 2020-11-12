---
title: Installing an alternative to Little Snitch for Linux, GUFW Firewall
layout: post
image: https://i.imgur.com/kUHRFop.png
tags: firewall, linux, security
permalink: /alternative-to-little-snitch-for-linux-gufw/
---

The GUFW graphical firewall is the only real user-space firewall available for Linux. It's comparable to the likes of Little Snitch for MacOS or GlassWire for Windows.

Installing and configuring UFW Firewall on Ubuntu, LinuxMint , Debian and all its derivatives, is a simple task but you have have some control over it.

In this article we will learn how to configure it from the console / terminal (server-oriented) and how to perform the same task using the graphical mode with GUFW (desktop/laptop PC).

The first thing we will do is install it, because although Ubuntu and LinuxMint is installed by default, Debian or Devuan does not.

## Easy Installation in Debian-based operating systems

Install GUFW with aptitude...

> sudo apt-get install gufw

Now activate it.

>> sudo gufw

## GUFW GUI Configuration

The location of the launcher can vary depending on the distribution you have installed, however the most common is: "System->Administration->firewall configuration".

It can also be launch from the command line as indicated in the step above.

![](https://i.imgur.com/5QUn7Ra.png)

Configuring GUFW is very straightforward, but you need at least the bare minimum of networking knowledge to setup more advanced configurations. Here is an example of me blocking all incoming & outgoing SSH connections.

![](https://i.imgur.com/qNUA2GD.png)

In the advanced tab, you can do amazing things like:
- block/allow port ranges
- black/allow ip address/ranges
- specify which network adaptor to use
- specify which protocol to use (TCP or UDP)

The best feature of GUFW is having a live log file to check within the user interface. If you are paranoid, I would recommend enabling full UFW logging under **Edit -> Preferences -> Logging: Full**
