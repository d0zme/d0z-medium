---
title: DNS Pinning Just Got Worse
layout: post
tags: dns
---

[Amit Klein just published a rather interesting article](https://web.archive.org/web/20130131012857/http://www.securityfocus.com/archive/1/445490/30/0/threaded) on how anti-anti-DNS pinning techniques can be circumvented (counter counter measures). Namely how you can get around Host: header restrictions by using XmlHttpRequest or by forging headers with Flash. Coupled with Martin Johns’ DNS pinning circumvention technique this marks a sad day for web application security for Intranet applications.

Now from any website in the world that I control, I can read your internal interfaces of your web applications and actually return the entire website. Of course this doesn’t reveal credentials, but it certainly will tell you everything you need to know from an unauthenticated state about what every Intranet page looks like. Ouch.

Amit explains that the common technique of looking for the Host: header on the server will not work against DNS pinning evasion. Previously this wasn’t that big of a deal because you can just go to any website that you want and from an unauthenticated state you can see the webpage. That’s not particularly interesting unless you can’t get to the website (in the case of RFC 1918 non routable address space). Combining these two techniques gives you the ability to read internal addresses. This might not seem easy to exploit because how do you know what a company names it’s internal machines? There are a few ways. First, you can do web searches for logs that may contain referring URLs from intranets. For instance, here are just few intranet servers I found out there:

The one that I think is the most interesting is actually Hi5 (even though this is also visible from the Internet-despite it’s name), because I think this is really sestemic of the issue. There are a few very common names for intranet applications that can help you get started in your recon. The first is “intranet” as Hi5 shows us. Being able to read the intranet website can help you locate lots of other servers because intranet applications are designed to be hubs where users go to locate other servers. There are tons of other common names, but I think you are best off finding the intranet application and spidering from there.

So, in review: Locating that the site is there in the first place using Jeremiah’s JavaScript intranet port scanner and then using the DNS pinning attack to read the page itself pretty much seals the deal.

---
