---
title: Detecting some forms of MITM attacks
layout: post
tags: mitm
---

There are quite a few different methods of performing MITM attacks, but one in particular kinda struck my fancy early on when I was thinking about airpwn. In the case of airpwn and similar exploits the attacker may be able to listen to the packets being transmitted but they aren’t able to block them, so instead it comes down to a game of beating packets to their source and origin. I don’t know what the prevalence of use of any sort of MITM is, but in this case there are a few things you could do to detect.

Anyway, if you receive double the DNS replies, or double ACK responses for instance, that could indicate that someone is trying to beat another packet back, which is why you’ll end up with two. Of course, figuring out which one is real isn’t straight forward (the bad guy may have just been slow, so it’s the first one that’s real). And there may be other things the bad guy can do like immediately forward a RST packet to the server you’re trying to connect to to quash the double ACK, so this may have some limits of utility.

Perhaps someone could think of another ingenious way to use that information or think of other clever methods of detection based on something similar for the other classes of MITM (like acting as a proxy, or re-routing traffic, etc…). I’m sure someone somewhere has already thought about and posted about this concept, but I wasn’t able to find anything in a cursory search. Maybe it’s new, maybe not, but I still thought it was interesting, even if limited.
