---
title: What are the odds of a small wordpress site getting hacked?
layout: post
tags: wordpress
---

The blackbox security analysis is worth discussing further, since I don’t think I went into enough detail on my last post, so here it is:

    Hypothetically speaking (no betting is taking place here, no sir) what odds would you put on your blog and why? Have you gone to any great lengths to harden WordPress here?

Hi, Andy, good questions, but I want to be very careful that I don’t confuse the two because they are very different questions.

What odds would I give on a wordpress site surviving a penetration test, verses some other website (say something large, like Google). Well, it’s hard for me to be objective and act like a bookie would on my own site because I know how it’s built, but let me try to pretend I know nothing about me as a person and the inner workings of the system and only use information that is already available on the websites or from other sources gleaned from the web.

Firstly, it is pretty obvious I am using WordPress, as you mentioned. It’s a free software application written in PHP. It has already had bugs found in it, and it is open source. Given that information, It’s got a fairly high percentage of finding further vulnerabilities in it (not knowing anything about what I have done to it). However, the fact that it’s had bugs and fixed those bugs does make it slightly more hardened, theoretically. It also has a MySQL backend, making it subject to MySQL injection if a vulnerability is ever found to exploit it. Thankfully, it appears I have turned off user accounts, so that does mitigate the risk somewhat, but beyond that, it’s not clear what I have done to it.

Next, it appears I have some CGI scripts on the site. It’s not clear what language I wrote them in, but I do mention PERL a number of times throughout my site and various posts I have made, so it’s a safe assumption it’s either PERL or some sort of shell scripting (bash or ksh). Let’s assume PERL for a second. Clearly these are not open sourced applications that I’ve written, and given my background in security, it’s a fairly safe assumption that security is built into it.

There are approximately 5 boxes in which to input data on the entire site, no cookies are set for my users, and it doesn’t appear that any information is logged and then exposed to the site with the exception of my clipboard stealing application which has already been unsuccessfully attacked dozens of times, so that looks pretty good. Now let’s look at the network portion. It doesn’t appear that the website communicates over any other port, which is good.

It makes only one known outbound connection (WordPress’ ping). So far so good. Okay, on to the people who maintain it. There are only two people who appear to run the entire site (id and RSnake). Both are self-proclaimed experts in their fields (RSnake in web application security and id in network and OS security). I’d give this a fairly low likelihood of exploit given that simple fact alone. What about the site history? The site has been around in one form or another for 5 years, and has not yet suffered one successful attack. Pretty good!

Now what about Google?

Google uses all homegrown scripts, it looks like. They are, however, suffering from the problem that most big companies have, which is that they have absorbed a lot of legacy technology from other companies via acquisition. That right there scares the crap out of me as a security guy as this was the sole reason for The Largest Hack in the History of the Internet (TM). However, it looks like they run the gambit of languages. Everything from Python, to C. That makes them a candidate for all sorts of varying exploits against the various types of applications.

They appear to be a Linux shop (albeit a hacked up version) from their TCP signatures and from what we can gather from the various white-papers. However, their corporate intranet is strewn with varying operating systems, with outdated versions of varying browsers. Ouch. Allowing access from the intranet out to the Internet is a recipe for disaster (banks have begun to disallow it, for a reason).

Google has just about every application a portal could want. Lots of them are tied in with databases. They have thousands of input boxes, they do set cookies, accept query strings, and god knows what else. They make outbound connections via translation services, their spider and mobile devices (among probably a dozen more). They speak a number of protocols, including HTTP, HTTPS, IMAP, + whatever Gtalk uses, among others. Plus they log and replay unmodified versions of webpages via Google cache (ever considered hosting a phishing site on Google?)! Also, almost all their applications are in beta mode, meaning they have not gone through the strict security quality assurance typically associated with productized applications (at least that’s what it looks like). What a mess!

Let’s look at their network now. Via aquisition they’ve ended up with this mass of websites. They have multiple data centers, and allow people to work remotely through VPNs from what I can tell from their network traffic. Yah, not so good.

Now, who maintains it? Well Google has literally thousands of employees, very few of whom have had formal security training. I don’t have any numbers on the size of their Trust and Safety arm, or infosec arm, but I’m picturing it in the sub 100 people range, if you discount Adwords ToS monkeys (which I don’t consider to be security). That means that for every thousand lines of code, maybe 1-10 sees the eyes of a security expert. The rest goes through automated scanning (I would presume), but we all know how effective that tends to be.

Lastly, let’s look at their history. They have had holes in nearly every application they have launched or aquired (Google Base, Gmail, Google Personalized Page) and at least two and maybe as many as 5 depending on how you count it have been found by hackers (yours truely). The scariest one (not found by me) was an unpublished one where every Orkut user got their account information stolen. Not such a good history.

Given that both applications are heavily attacked by assailants, and that some of the holes found in Google were found by the webmasters at us, I would give the odds 1:300 against me getting hacked before Google.com was, given the same time and resources. If I were a bookie, my money would be on Google to loose. I’m not saying Google has shoddy security. I’m actually just going with what I can see from the outside trying to stay as objective as possible. That is completely trying to stay unbiased, pretending to not know the reality of this stie and without knowing the inside of what Google really looks like.

Okay, I hope that answered your first question. Your second question is actually quite a bit harder. Wordpress is a crazy beast. Without going into lots of specifics about what I’ve done to it, let’s put it this way. I am more careful about protecting the server from Wordpress than getting WordPress to protect the server, if you catch my meaning. I have modified WordPress though and if I had more time I would do a complete re-write of certain sections of the code (maybe in the next few weeks I’ll find some time). Honestly, I know there are about a half dozen places that desperately need re-working, but I have’t had enough time to read the code thoroughly. I did do a rough first pass, and that’s why I bothered to install it at all (it passed the gloss over test), but it certainly doesn’t meet my needs as a hardened CMS (yet). That said, it’s by far the best I’ve seen.

Now, to the question you’re really after, would I consider wordpress to be 100% secure? Nope. Not even close. But security isn’t about 100% certainty. It’s about risk mitigation. If I got hacked into, what do I risk? I don’t make any money off of the site anyway (a few bucks but let’s be real). Maybe I get some of my readers laughing at me, but at the end of the day, it’s probably not going to be code that I wrote that caused it anyway - giving me some plausable deniability. But what I will say, is that given the nature of this site, for some reason people think it’s okay to attack it. Some days we can see up to hundreds of attacks against the site, and not once has anyone sucessfully penetrated. Not bad, I’d say. id is a bad-ass networking guru that keeps the network attacks at bay, and I keep the site’s front end exposure to vulnerability to a minimum. It’s a proactive game, and I modify the site on a daily basis when I see a problem arising. Will we get hacked into? Probably some day. But I’m not too worried about it.

---

