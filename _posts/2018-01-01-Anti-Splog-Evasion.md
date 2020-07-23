---
title: Anti-Splog Evasion
layout: post
tags: spam
---

I know I’m really going to kick myself for this one, as it will no doubt come back to haunt me, but I’ve been thinking about this one for a long time. One of the things that Blackhat SEO types do is they attempt to scrape other people’s sites that have original content (such as mine). Then they post that content on their site as their own, attempting to raise their own page-rank. Because the search engines aren’t smart enough to know who is the original author, the sploggers get higher in the page ranks.

One of the tactics to evade them is to deliver unique content to them (a one time token or something of the like) that allows them to see the content, but if they attempt to replay it, the webmaster can tell who it is by going to their lookup table and seeing who scraped them. Often times you can shut them off at the source or do something more evil like I did. But there’s a way around it.

![](https://i.imgur.com/JZTfgeY.jpg)

If you click on the image you can get an idea of the concept. The concept revolves around using more than one scraper (which is not a new concept - see splog hubs for more details - but that’s only been used to hide the real IP address in the past). The difference between that method and this method is that you use more than one scraper and then validate that the responses are the same. If they are, you’re good, if they aren’t the same (because there is a unique token in the content) the content can be either thrown away or the splogger can attempt to clean it up.

This would make it much harder for sites to protect themselves from sploggers attempting to steal copyrighted materials. So why am I writing this? Because I still have a few tricks up my sleeve to stop sploggers, but I thought it should at least be known that there are ways around some of the more obvious protection mechanisms.
