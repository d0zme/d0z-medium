---
title: Detecting Spiders is the key to SEO
layout: post
tags: seo
---

One of the major problems in blackhat SEO (search engine optimization) is detecting what is a robot and what is a user pretending to be a robot to detect what you are doing. There are a lot of tricks out there, but almost all of them can be subverted. It would be interesting to catalogue them and see which ones work for what, instead of just trying to keep them all in our heads at one time.

IE: User Agent Detection -> Works for all search engines that don't lie or change their user agents. Doesn't work for when competitors change their user agent and pretend to be a spider. Etc...

---

For googlebot, you can verify that it is googlebot, rather than someone spoofing the User-Agent, you can do a reverse lookup, as is described here: http://googlewebmastercentral.blogspot.com/2006/09/how-to-verify-googlebot.html

Of course, this results in the problem of potential DoS attack (probably not too likely, but still possible), since doing reverse DNS lookups (which actually involves two queries - one to get the host name, and then one to verify that the NS responsible for that name returns the IP you are checking) isn't exactly a cheap operation.

I've been planning on sending google an email to see if they can either provide a list of domains somewhere, or get crawl.google.bot.com to return a list of all the IPs which googlebot has, but I'm lazy and forgetful......

So the only real solution to improve performance that I could come up with is to manually hard code the netblock in which google resides (or just use 64.*.*.*-66.*.*.*), and then only doing reverse lookups only if it is that range.

Oh, and of course add all IPs which don't have the appropriate reverse DNS results, or aren't in the net block just get added to hosts.deny or to your firewalls rules, so that you don't do the same request over and over from the same IP and so users have to use proxies to attempt a DoS, and that should stop it. Furthermore a caching system with a list of Googlebot's current IPs would also speed things up, there's a fairly recent list availiable here: http://johnny.ihackstuff.com/index.php?name=PNphpBB2&file=viewtopic&t=3418

I have no idea how to detect other bots, but if you know which bots you want to allow through you could compile a netblock or IP list.

Me and a friend are working on a paper (err, more being lazy and not writing up our ideas, than anything, but its coming) about how to detect bots and some other things, hopefully we'll get around to finishing it soon enough, and once we do I'll add that here.

---

DNS reverse-lookups and anything source IP based can still be spoofed from IP/ASN hijacking and a few other methods. Spammers, click-through fraudsters, phishers, and blackhat SEO are already using these methods as well as um... proxies.

The key to detecting bots is going to become similar to detecting someone using ippersonality or Tor. Most of the current techniques seem to be kernel timing based, which is also one of the best current methods to detect rootkits.

I am still looking for running code that makes my bots look like undetectable humans. Billy Hoffman did an interesing presentation on Web Crawling but SPI never released the code.

---

