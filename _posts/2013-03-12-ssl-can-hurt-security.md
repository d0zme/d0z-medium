---
title: SSL Can Hurt Security
layout: post
tags: ssl
---

SSL can actually harm web application security auditing and intrusion detection. In fact, SSL can actually make it next to impossible for you to do forensics in the aftermath of a successful penetration, or brute force.

Once upon a time, man in the middle (MITM) attacks were rampant on the net, or so security experts would have loved for you to think. Then public key cryptography (PKI) and digial certificates in the form of x509 website certificates came along. The world rejoiced and there was much merry. But what happened to those MITM attacks? Have they gone out of existance? Hardly! Much to the glee of every blackhat out there, more and more people are tunnelling what should be secured information over insecure protocols (how many times have you recieved your recovery password over mail for instance)?

But let’s take a step back for a second. SSL was once upon a time a great idea. Most of the hosting community was comprised of small mom and pop ISPs with little more than a T1 into their offices. At that time, your peer was probably just as small and insecure as you. And besides that, the net was a very small place, made of only a few thousand websites. Along came PKI and the sudden boom of the net taking the few of us who were already online at that time, by storm.

Now the net looks very different, being seperated by huge nodes of private companies who take network security very seriously - and besides, network security is so 2 years ago (okay, I know I’m going to get shot over that one). No, but seriously, these major ISPs have got their act together a lot more than the mom and pop’s of yesteryear. Sure, you can still ARP-spoof a switch, or exploit a router here and there, but in large part you are far more secure using the net then you were a few years ago. But why? Well, think about how many hops it takes to you to get from your house to the bank of your choice.

Unless you are in some ultra rural location with very dodgy connections to the web via modem, you are probably on a high speed DSL, connected directly to your provider. That company has peering aggreements with major telcos. Those telcos have aggreements with other telcos, and those telcos host your bank. Where exactly would a bad guy have to be to steal your information? Well these days, it’s really no different than it was 10 years ago. It’s still your first hop that’s the least secure. Me connecting through my wireless connection at home is far more likely to get my information stolen by a MITM than me connecting through the next 6 hops.

Okay, so back to SSL. Where is it useful? The first hop, sure. But it’s also helpful for the bank, right?  They know your information is safe, so they are less likely to pay out, if your information gets stolen, right?  Well, sure, but are they going to be able to capture that information? That’s only vaguely useful to the consumer since MITM attacks are far less used than they used to (which may have had something to do with SSL - I admit). Let’s take another example.

What if I am joe-small-website with a mechant account, and a I sell snowboards through my site? I may have an IDS sitting out in front of my website, but that’s probably all I can afford. Now, I’ve got SSL sitting on 443 and port 80 serving the normal site traffic. Once the user goes to check-out, they are off the radar for my IDS.

So what if I’m a bad guy? Well in that case, that’s even better. I can now evade some security by actually using a security mechanism to do so. Unless they have an SSL accelerator in front of an IDS, I’ll walk right through their security. Ultimately, they are now more vulnerable because of their SSL than they were before without it, while only providing a small amount of protection to their users in doing so.

That said, do I use SSL? Of course! You’d be an idiot not to. Duh!
