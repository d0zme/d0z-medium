---
title: Detecting Privoxy Users and Circumventing It
layout: post
tags: provoxy
---

TOR is a pretty cool idea. It’s partially a rip off of a very old project that I helped out with in it’s inception with a bit of peer to peer built on top of it to help with anonymization. Anyway, very cool. Very slow, but very cool. From what I’ve been told it’s mostly for people looking for beastiality porn, but you get the idea. It’s got all kinds of applications. But it’s a little disconcerting that I don’t know if my users are hiding their origin IP addresses. Wouldn’t it be nice to be able to detect that?

So anyway, there I was, downloading the torbutton extention which requires Privoxy and TOR to be installed. Like a good little security guy I go and locate the current version of TOR which is thankfully bundled with Privoxy. I booted it up and after some wrestling I got it working. The first link I went to, however, was a tad puzzling. It was my own.

My own website has links to ads in it, which Privoxy so nicely kills with an error message letting me know why, and allowing me to go directly to the link. That link that allows me to bypass the Privoxy block was intriguing as it was just a modified URL (and a pretty easy one to reconstruct at that). So I threw up a little test script to detect privoxy and poof! I inserted a keyword that it blocks after a legitimate image with the modified URL. If it hits it, Privoxy is being used. If there’s an error because it’s not finding the correct image (because the modified URL doesn’t actually exist) you know they are safe. Now I can tell if users have it installed or not. This may be better than the chrome:// firefox extensions detection because I have a feeling that will get killed eventually.

---

My guess is host countries are going to start harassing these anonymous proxies in a big way. It makes law enforcements job much harder. Most countries won’t outlaw the practice but with enough subpoenas, warrants, and associated server seizures (temporary as they may be) no one is going to want to run them. The free one’s are especially vulnerable. The paid servers may initially try to survive by allowing law enforcement to install traps so they can sniff traffic at will. But once that is known few people will want to use them.

I know there are legitimate uses for these services, I’ve used them myself. But when you have a high percentage of people using them illegally you can guarantee LE will take notice and the politicians will thump their chests and pass laws restricting them. The German TOR seizure is just the beginning.

---

General purpose servers such as those being used by Tor cannot be shut down. Why? Because all traffic is encrypted so the State has no evidence against them. An of course there is the freedom of speech/information.

But even if in some country, let’s say North Korea, they decide to shut down the servers in their domain, no damage will be done since we are talking about a P2P architecture. Every user is a potential Tor relay server and the routing circuits are constructed in a random way. In the worst case scenario your traffic will be rerouted across the globe to access a neighbor network but that’s not the point. The point is that it WILL be rerouted :)

You can’t shut down P2P.

@RSnake: You may be able to detect whether the visitor is using Privoxy but you can’t be sure about his IP. I mean Tor operates in such way it is possible he IS using his real IP (the circuit is user-client -> user-server instead of user-client -> 3rd-server1 -> … -> 3rd-server-n -> www.target).

Also, I understand what you are saying but I haven’t been able to reproduce it using Tor+Privoxy as standalone applications (not using the Firefox Plugin).

---

