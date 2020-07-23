---
title: DNS Rebinding in Java
layout: post
tags: java
---

[Stefano Di Paola](https://web.archive.org/web/20150315044043/http://blog.mindedsecurity.com/2010/10/dns-rebinding-on-java-applets.html) has an interesting article about DNS Rebinding in Java. Apparently he’s found a way to bring back some of the older exploits that were supposedly fixed in Java back in 2007-2008 timeframe. Really cool read. Half way through reading it I realized that this would enable exploits like the one where sites often have localhost.whatever.com tied back to 127.0.0.1. The old exploit worked in that if you could ever find an XSS in a local service you could set cookies for whatever.com domain, or read any cookies that were set to the entire domain. It’s a nasty exploit, but rare because there don’t tend to be a lot of local services installed on desktop computers that are vulnerable to XSS by default.

Then I kept reading and he enumerates that exact use case - great minds think alike! Anyway, this apparently will be fixed in a future update, but now that we’ve seen DNS rebinding hit Java twice, I think Java needs to have a much more critical eye. Things like this shouldn’t be sitting around for years before they’re noticed. Like inter-protocol exploitation this research needs a lot more eyes. Great work by Stefano!
