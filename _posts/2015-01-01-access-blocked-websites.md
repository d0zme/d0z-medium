---
title: How To Access Blocked Websites
layout: post
tags: network
---

I happened upon an article last night talking about how to access blocked websites. First of all, this is sorta missing a major component that most people are actually concerned with, which isn’t just how to access it, but rather how to access it and not get caught. Generally you don’t want to be accessing a website through a content filter and still set off alarm bells. The content filters in place are set up by governments, your place of work, your school or otherwise people who can negatively influence your life for looking at questionable websites.

Let’s walk through the list on that website and punch a few holes in it:

First they say to use anonymizer. Anonymizer is almost always bocked by content filters, so forget that one. Yes there are anonymous CGI scripts out there, but if your content filter works on keywords this is pretty much out.

Secondly they say to type the IP address of the website in. Okay, but how did you find out the IP address of the website? Presumably you did an nslookup on it? So now you have to ask yourself is your content filter watching outbound traffic on port 53? Or are they looking for strings like “nude” “xxx” “bombs” or otherwise sniffing the unencrypted traffic? Are you querying their name server or your own? And lastly, is the website in question even listening on an IP without requring you to send host headers? If they wanted to stop you from doing this, it would be very easy to do if this is the only trick you used.

Third he says use tinyurl or other redirection services. I don’t see how that could possibly fool a content filter. He’s claiming that the URL bar doesn’t change. Either it’s embedded in an iframe or otherwise concealing the page that is being rendered. That doesn’t mean your browser isn’t sending HTTP headers that the content filter can read. This one is just flat wrong. Beware people saying that redirection services make you secure. They don’t. At best the hide the referring URL (META refresh), at worst they do nothing (301 redirection).

Fourth he says to use Google Mobile Search. This is probably one of the few that might actually work, assuming the content filter isn’t keyword based. I won’t talk negatively about this, except that it is a really hobbled experience, and will dramatically reduce your browsing experience.

Fifth he says to use the cached version on Google or Yahoo. Ouch. A) keyword filters will still pick this up, B) Guess what, Google doesn’t cache any embedded content, so you still send headers for the images, the CSS, the JavaScript and any other embedded content, all of which will be blocked, if the content filter is set to be indistriminant about the file types (which most are). You’ll definitely get caught doing this.

Sixth he suggests using Google’s translation service. This has all the same problems as the cached version. Don’t use it for actual privacy.

Lastly he suggests using a proxy server. If the content filter allows you to use a proxy server and it is not the proxy server itself, this might work, assuming there are no keyword content filters. I mean, really onion networks work on this premise, but we’ve proven that this is a pretty easy thing to detect in some recent conversations on sla.ckers.org due to the fact that the tor networks have been mapped. Still, this might be your best hope.

There’s some end comments on that page discussing issues with the Chinese firewall, which clearly he doesn’t understand as the Chinese firewall primarily works off of keyword filters and is trivial to evade, and it’s not particularly relevant to the discussion anyway. If you want to evade the chinese firewall use peekabooty, Tor or SSH forward your connection, or simply rot13 everything because it cannot detect even the most simple obfuscation.

Anyway, I’m not trying to pick on the guy, but there is a lot more to anonymous surfing than meets the eye. Don’t take advice on anonymous surfing from people who don’t understand how the Internet works. Especially if your job or your life depends on it.

---

