---
title: Preventing XSS Using Data Binding
layout: post
tags: xss
---

Using data binding he can make JavaScript attach user content to the page while validating that it does not contain active content. That is, styles are okay, but JavaScript is not. Very interesting. Here’s the demo (warning, not for the technically feint of heart).

Stefano asked me to give my report on the good and the bad. The good is, this is pretty damned good at stopping XSS. It probably won’t stop abuse of styles that position themselves over other people’s content, but it would stop a good deal if not all XSS if implemented properly. That’s the good news (and that’s very good news for most people). Here’s the bad news.

The bad news is that it requires JavaScript to work. If you don’t have JS installed, forget it. That’s bad news for security people, bad news for accessibility, and even worse news for robots who are trying to get contextual understanding of the page. It also forces the bottom of the page to be where the user generated content is. That’s also bad for SEO because it means the most relevant content is at the very last part of the page. Depending on how the page is built and the spider, this may fall off the size limits of the robot. Not good. Lastly, it would reap havoc on lots of those poor web application scanners. They would light up like Christmas trees because there is NO output encoding done. None. Zip. It’s funny to make web application scanners have false positives, but it’s also a pain in the butt if you’re the operator of said scanner. Herein lies one of the advantages of scanners that use built in rendering engines (forgiving any other issues they may have).

So where would this be useful? Think about all those web2.0 applications out there that have to put dynamic content on the page, don’t have to worry about spiders, robots, and need to make sure that what they output is okay no matter what encoding, or any other craziness that users may put in. I’m not advocating being sloppy, and there may be other issues here that I haven’t found, but thus far, it’s looking like a promising technology.
