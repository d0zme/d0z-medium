---
title: JavaScript Port Scanners
layout: post
tags: javascript
---

In case you were living in a cave the last few days or aren’t subscribed to any of the security mailing lists out there, you probably already have seen these links but I’m putting them up here anyway. First, SPI Dynamics released their version of what Jeremiah is working on (although not nearly as feature rich, it does isolate one of the various things Jeremiah will be discussing in his speech at BlackHat). [This is in an Intranet port scanner](https://web.archive.org/web/20130107093008/http://www.gnucitizen.org/projects/javascript-port-scanner/) written in JavaScript. Then a few days later PDP (architect) released his tool which did internet port scanning in JavaScript (which is not what will be covered by Jeremiah’s talk so it is actually slightly different, although using the same ideas).

Both of these tools don’t go into most of the problems that we were able to overcome, because they weren’t working with our original idea - they took it and built their own based off the idea (despite what the press releases claim) which can be proven by the fact that I’ve been talking about this publically for months and have been working on it for most of this year. Oh well… at least the rest of the world knows the truth. I’m not really into conspiracy theories, but read SPI’s paper (the first paragraph) and then read Jeremiah’s talk overview and tell me that idea is legitimately theirs. It’s a little disheartening that security companies are stealing ideas. As if we don’t have enough actual bad guys to battle. Alas.

Anyway, despite the immaturity going on, this is a really exciting time for cross site scripting, as we are uncovering all sorts of new practical applications for it. I see this as a doorway project, that will lead to all sorts of interesting development in cross site scripting malware. I, for one, am excited!

### Comments:
---

Exactly! And even if you trust the site you’re on, it doesn’t matter if they have XSS issues. It’s almost at the point that there’s no hope. Personally, I’ve taken to keeping JavaScript turned off unless I know exactly what I’m going to be going to and exactly what the site function does. That goes for Java completely these days. I use Firefox for my day to day surfing so Active X isn’t an issue, and neither is VBScript. It’s getting close to the point where we go back to straight .html files if we want to get our security back in order. That’s obviously not the answer, but I haven’t heard any other good answers either.

---

The basic principle is if the port is open it will give an error and you can trap it, if it is closed you cannot trap it. That’s the basic idea. There’s a lot more to it, obviously, but that’s the basic premise. It gets really confusing when you get issues like Firefox’s blocking of certain low ports, but we found ways around that. I can’t spill the beans but that’ll be part of Jeremiah’s stuff.

---

To be honest this concept isn’t groundbreaking, it is putting common sense idea’s together. I came up with this a over 2 years ago however didn’t look to post it anywhere. You need to understand that people in a certain field come to the same conclusions. You stated yourself it isn’t as feature rich as yours, perhaps validating it isn’t a direct copy. If it was a direct copy it would be MORE feature rich than yours wouldn’t you think? I mean if it was copied to ‘get fame’ wouldn’t the extra effort be made to jazz it up a little so that it would be the only one talked about and not yours?

We’ve all had people publish things before us and it fucking sucks, however you need to understand not everybody reads your blog or 1 entry on an OWASP site (aka a wiki), and that shit happens to everybody. It isn’t always intentional and when a company is involved the chances of it NOT being a copy is greater being that their bottom line would be affected and questioned which is bad for business.

It sucks but whatever, move on come up with something else, and do what you want with it. Probably 20 people have actually started writing code for this idea, however maybe half of those did it on almost the same lines.

Either way props to you for discovering it on your own.

---

Mr Barf, thanks for your post. You made some incorrect assumptions that I’ll try to clear up for you. First, since your email and website are both fake, I’ll just have to pretend for a moment that you don’t work for SPI yourself (probably not a good assumption). Without any proof to validate your claim that you came up with it on your own, or even who you are, I’ll just have to trust that as well. I’m not sure why you wouldn’t publish it if you came up with it. Maybe I’m seeing more of the destructive potential than you are. I understand people come up with the same thing as other people, really, trust me. I’m not an idiot. However, the timing was just too perfect.

Sorry, but the SPI guys definitely read this blog, and the mailing lists where it was also mentioned (as do you, obviously, as I didn’t mention the OWASP post in this blog entry) as do a lot of die hard webappsec folks. SPI Dynamics knew about Jeremiah’s talk and they even mentioned it in their paper, although didn’t give it credit in their press release - instead saying they invented it. If you really came up with this two years ago, you should be annoyed with them too. Sorry, that’s just unethical. Mistakes happen, but that’s not a mistake.

And no, your logic is flawed. Just because they copied it doesn’t mean it would be as good. A) they were going on small bits of information and B) they had less time to develop a polished product. I would be amazed if they had built the same thing in the time they had to rip the idea off. Look at PDP’s page… it’s even less polished than SPI’s page (less time, less information). Stands to reason that SPI’s demo looks and acts exactly as it does based on that same issue.

I’m not really that miffed about it, Mr. Barf, I think you’re reading into this a little too much, but I am surprised that anyone would be so blatant about it. I’m not out to destroy SPI or anything, I just think credit is due where it is deserved. If you spent the last several months working on something just to have a random company leap on your idea and build it a week before you were going to unveil it wouldn’t you bring it to the public’s attention? I had the option to keep quiet and let SPI take the spotlight, or let the public know what really happened. My way is the truth as I see it - I don’t know why anyone in the world other than a SPI employee would be upset by that. What pain have I caused you to post this? Did I touch a personal nerve, Mr Barf? Interesting.

Anyway… I let this post through moderation because I think you have some points that needed to be addressed, but let’s keep the teenaged flames to a minimum, shall we? We’re all professionals here.

With that said, you are welcome to post here anytime, using whatever pseudonym suits you. Mi casa es su casa.

---

