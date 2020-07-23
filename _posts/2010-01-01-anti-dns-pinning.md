---
title: Anti DNS Pinning Without Using a Firewall
layout: post
tags: dns
---

[Kanatoko](https://web.archive.org/web/20150320094409/http://www.jumperz.net/index.php?i=2&a=1&b=7) found a vulnerability in the DNS pinning used withing modern web browsers that can be exploited by simply shutting down an open port. This is far easier than the previous technique of closing the connection using a firewall. Very tricky. Kanatoko also pointed to another issue disclosed on bugzilla as well regarding another anti DNS pinning technique.

To paraphrase the user connects to my machine which has an IP address of 123.123.123.123. I use a Dynamic DNS server that tells the world that mydomain.dyndns.com is located at 123.123.123.123. When my DHCP lease expires I move to another IP, dyndns.com points to it and the rest of the world can now find me. The one poor sap that was on my page already and has DNS pinned my IP address will now submit their content to whomever takes over my IP address next, assuming they do so before the user is finished submitting the form (otherwise their DNS cache will flush and they’ll move on).

This is a tricky way for DynDNS users and other dynamic DNS users to compromise information from other servers. Of course it relies on the person who had your DNS entry before you a) having a webserver with forms and b) having traffic you’d want to compromise (since this is blind there’s no way to know ahead of time if you are interested in that traffic). Normally this wouldn’t be a problem for most websites because they don’t use this sort of DNS hacking, but it does point to some major flaws in how DNS is implemented and not necessarily just another browser flaw, as Kanatoko pointed out. Great find!

---

