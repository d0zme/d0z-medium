---
title: Myspace was a hotbed for 0-day exploits
layout: post
tags: exploits
---

I laughed out loud when I read this. Kuza55 found another issue in MySpace again today using the exact same exploit that we have been trying to get them to close FOUR separate times now. Click here to read about the XSS hole last time if you don’t recall what I’m talking about.

Anyway, this is the exact same non-alpha-non-digit issue that they have faced numerous times before. Only this time they got exploited through a different issue they caused for themselves. Remember how I’ve said a number of times don’t strip content unless you really know what you’re doing? Well they don’t really know what they are doing (if you aren’t using a while loop you are already in trouble). In this case, they stripped out moz-binding (the Firefox CSS issue) and replaced it with “..”. Wellll if you make your vector look like onloadmoz-binding= and it gets replaced with “..” you get onload..= which still works in Firefox.

Kuza55 said it best… you really have to wonder what these MySpace developers are thinking right about now. Anyway, this is why you should never ever strip or change HTML input unless you know how HTML works in different browsers, lest you get hit with the same issue 4 times. Nice job 
