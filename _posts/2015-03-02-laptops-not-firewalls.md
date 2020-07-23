---
title: Laptops aren’t firewalls
layout: post
tags: network
---

As if you needed another reason to visit Blackhat this summer, two researchers just found a way to hack into wireless cards remotely and take over laptops. David Maynor and Jon Ellch will demonstrate it in August, at the convention.

This is really the problem with how companies treat laptops.   People are given laptops to be more mobile, which is great, but they are protected by the systems that no one in thier right mind would put on an unprotected network.   Then they are allowed to go out into the world and log into whatever network they choose.   Obviously this is a perfect time for viruses, trojans, keystroke loggers and malware of all variety to infect the machines.

The problem is peoople treat laptops like corporate firewalls.   If there is an access to entry, the bad guys will take it.   It’s really not that hard either.   Keeping a system dormant or sending out one packet once in a while until you find it omitting packets from an interesting network, is pretty trivial.   Treating corporate laptops as the front line security, but then not adding additional protection on top of them seems like asking for disaster to strike.

Of course, the wireless protocols that exist today are all prone to insane problems.   If you read the article on the six dumbest ways to secure a wireless LAN you know that there are a half dozen obvious problems with configuration, and probably an equal amount of tricks to get access, like spoofing access points, attacking the access point directly, cracking WEP, etc…   And that’s without even doing anything to the laptop itself.   Now, you add on the ability to hack the basic fundamental peice of hardware that can secure the transmission of data to your network, and you have a clear path to gaining access to that network.

Of course there’s more to it - there are way more protocols than just 802.11b that are at risk here. People have AIM/YIM/IRC sessions, email, NNTP, HTTP, and god knows what else.   All of which are viable transport mechanisms for malicious users to gain access to the laptop, which sits well behind the DMZ.

I had lunch with the CSO of a big bank at one point and he said the best advice he ever got to securing a large scale network was from a guy at Gartner who told him to “not let the local admin rights genie out of the bottle.”   I think that’s the right first step, but taking it further, allowing the user to have any access to the network beyond what is “safe” and secured seems like a bad idea.   Not to mention that 70% of successful hacks attempts are from employees anyway.

So anyway, go to Blackhat, and listen to Jeremiah Grossman’s talk as well as David Maynor and Jon Ellch’s talk if you get a chance.   I bet it’ll be interesting.
