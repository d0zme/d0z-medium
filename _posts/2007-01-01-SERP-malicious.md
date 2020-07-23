---
title: Malicious SERP Arbitrage Lessons
layout: post
tags: seo
---

I spent the better part of my free time for today putting together a rather sophisticated search engine result page arbitrage tool. No, I won’t release this one. Partly because it sucks, partly because it requires that I allow other companies to run JavaScript on my domain, partly because it requires redirection, and partly because it’s easy enough that anyone with enough skill could do it themselves anyway. The point is I did it as a demonstration for a potential client, and there are some lessons learned. This is pretty nasty tool for blackhat SEO/SEM types.

If you don’t know what I’m talking about, it was an old trick I talked about revisiting, which is making the back button on browsers change functionality (popups or redirection to other sites). Only my version actually mimics the search engine the user came from.

1) The arbitrager must understand that the user is coming from a search engine. There is more than one search engine. So they must code for each one that they want to steal traffic from. This alone can be a bit of a nightmare.

2) The traffic arbitrager must detect which links the user has already been to so to make sure that if they are to click on those links again they end up on the page they meant to go to. This will make it fare less likely that the user will notice the trick. This is harder than it sounds because each site has a different style for the a:visited tag. And btw, case matters if there are any letters in the color (EG: 4e4e4e is different than 4E4E4E4E).

3) The site must take into account crazy JavaScript and Style sheets that all the search engines SERPs add to each of their pages. That can really mess things up (and definitely change the layout slightly). I defaulted to the no JS view that looks close enough - less likely to cause errors.

4) The first time the user visits you need to redirect them to the original page they meant to go to in question. If the cookie (state) exists where they have already been there, when they hit back they see the fake SERP.

Ultimately I think this is a pretty powerful tool for malicious arbitragers. Pretty nasty, actually.
