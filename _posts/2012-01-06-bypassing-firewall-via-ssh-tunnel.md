---
title: Bypassing Firewall Restrictions Via SSH Tunneling
layout: post
tags: network
---

Bypassing Firewall Restrictions Via SSH Tunneling

I ran into this article about Bypassing Firewall Restrictions Via SSH Tunneling which is actually pretty similar to something I wrote on tunneling Trillian Pro and then id rewrote to more broadly cover the topic. Whatever the case, this is a really invaluable technique if you aren’t already aware of it for bypassing content filters.

I’ve run into this all over the place - schools, libraries, offices, internet cafes, all of them are the same. They may have different reasons for it (protecting intellectual property or protecting kids from the evils of the Internet) but the technique is all the same. They all use content filters that rely on direct regular expressions. Regex is great for some things. For detecting abuse traveling over a network while watching only on the network? Not so much. SSH is a great way to proxy your connection through a network without being stopped. Actually in some rough initial tests, I played with some simple content filters and they couldn’t even “decrypt” rot13. Then I just got silly and started using piglatin. Anything you do will go right through, unless of course, you are trying to get to an IP address that you can’t obfuscate and they have a pattern for.

That’s when proxying your connection comes into play. Now you just load up your ssh client, connect to your external host with the web proxy server (serving only localhost traffic) and you port forward your connection and poof, you’re now bypassing anything you like. It’s really practical for when you are going out to a customer premise and you need to connect outbound but everything under the sun is blocked. Maybe even outbound port 22 is blocked, but if you put your external SSH port on port 80 you can walk right through those primitive network defenses. I mean, if content filters can’t stop pig latin, what hope do they have against AES or Triple DES?
