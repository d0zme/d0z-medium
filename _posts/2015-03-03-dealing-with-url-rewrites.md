---
title: Dealing With SEO/URL Rewrites
layout: blog
tags: seo
---

I've been thinking about how spiders work in the context of black box web application scanners.

On a very basic level all the spider does is regex for href attributes which are part of the same domain, enqueues them, visits them and so on and so forth.

There becomes a point when there must be a cut off point, and you simply can't follow every href forever. This is partly achieved by setting link depth, keeping a memory of the depth of the links checked and go no further than the cut off point. This helps set a certain limit, but with link depth alone, a spider can still take a hell of a long time to complete.

What if the following scenario happens:

> http://www.example.com/date.php?day=1&month=1&year=2011
> http://www.example.com/date.php?day=2&month=1&year=2011
> http://www.example.com/date.php?day=3&month=1&year=2011
> http://www.example.com/date.php?day=4&month=1&year=2011
> ...

Our link depth would be rendered useless and we would be potentially stuck in an infinite loop as the day/month/year values continue increasing until PHP hits some type of limit.

To resolve the above problem we simply only visit a certain path/page x amount of times. If we have seen the date.php page more than 20 times, move on, don't visit it again. That solves that problem.

Now. This is where my my question lies.

We have some Search Engine Optamisation at play with url rewriting.

So, if we take the above example url, we have:

> http://www.example.com/date.php?day=1&month=1&year=2011 => http://www.example.com/1_1_2011.html
> http://www.example.com/date.php?day=2&month=1&year=2011 => http://www.example.com/2_1_2011.html
> http://www.example.com/date.php?day=3&month=1&year=2011 => http://www.example.com/3_1_2011.html
> http://www.example.com/date.php?day=4&month=1&year=2011 => http://www.example.com/4_1_2011.html
> ...

Now, again our spider will get stuck in an infinite loop.

The one solution I have thought of is the following but not sure if it will work or if there are better ways of doing it.

We strip all non html tags from the html response body, create a hash and then use the hash to compare all future pages against, if we see the hash more than x times, move on, don't visit again.

Is this how web spiders overcome the above problem?

the hash value of two pages will almost always vary if only one single character changes. Stripping all HTML elements will not help here. Using hashes can be a way to detect exact duplicates of pages, but it will fail to detect near-duplicate pages. Search engines will be very interested in crawlers that can detect near-duplicate pages as good as possible.

Here are some links, that may be helpful or give some insights:

To infinity and beyond? No! - Google Webmaster Central Blog (August 2008)
Discusses the problem of "infinite spaces", like calendars.
http://googlewebmastercentral.blogspot.com/2008/08/to-infinity-and-beyond-no.html

Google Patents, Updated - William Slawski (February 2011)
http://www.seobythesea.com/?p=5114
Huge collection of links to Google patents, the section "Duplicate Content Patents" contains also patents on near-duplicate content detection.

Duplicate Content Issues and Search Engines - William Slawski (June 2006)
http://www.seobythesea.com/?p=212

New Google Process for Detecting Near Duplicate Content - William Slawski (February 2008)
http://www.seobythesea.com/?p=999

In the last article I found a link to a paper by Michael O. Rabin (from the Rabin-Miller-Test): Fingerprinting By Random Polynomials
http://www.xmailserver.org/rabin.pdf

I hope that there is something that you find helpful. Bill Slawski's blog is generally a good ressource on search engine patents.
