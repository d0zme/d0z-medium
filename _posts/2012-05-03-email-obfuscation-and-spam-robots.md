---
title: Email Obfuscation and Spam Robots
layout: post
tags: email
---

I’ve long been interested in spam and robots that scrape for email addresses. I’ve done tons of work in the space, although I’ve never published any of it. Call it more of a side hobby than anything I really want to go public with - as it is with a lot of my research. But anyway, today I was messing around with search engines and I found myself typing “at gmail dot com” into them for no apparent reason and poof, out popped a ton of valid although obfuscated email addresses. Aside from the raw text here’s a sampling of the different types:

    …<at>gmail<dot>com
    …(at) gmail (dot) com
    … at-gmail-dot-com
    … {at} {gmail} {dot} {com}
    … [at] gmail [dot] com
    … “at” gmail “dot” com
    … at-gmail-dot-com-for.info
    etc…

I think it would be interesting to create a generic algorithm for de-obfuscating email addresses of this nature. I’m sure it can be done to some degree, but some get more complicated, and I’m sure once you add in the variants of the username it gets even more complex. Even if you could get only 80% that would still be quite a feat. Still though, I have a feeling it wouldn’t take much effort to create a robot that made quick work of all those obfuscated email addresses. Of course, the benefit to a spammer in spamming people who proactively try to protect themselves from spam is questionable, but it’s still interesting.
