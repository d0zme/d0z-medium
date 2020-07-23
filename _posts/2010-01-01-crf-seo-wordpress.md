---
title: WordPress SEO CSRF
layout: post
tags: seo
---

Well, it’s with a bit of a saddened heart that in the first few minutes of checking through the WordPress code for CSRF I found my first vulnerability. I sat on it for a week or so until I had time to thoroughly test it, and sure enough, WordPress is vulnerable to SEO related CSRF. …and then the splogging community rejoiced. This isn’t such a bad issue from an XSS perspective because WordPress does a pretty good job of protecting it’s users from being able to inject malicious JavaScript, but it definitely does allow any content you desire to get indexed.

So here’s the scenario. I’m a webmaster with a blog (I actually am one, so it’s not a stretch) who happens to get lots of blog comment spam. Like a good webmaster I mark it as spam instead of deleting it because I don’t want them to be able to submit the exact same content again. The spammer themselves can actually see the unique identifier of the spam post by looking at the page. They see something like “comment-3182″. They file that away for later. On with the spamming they go. They can spam several thousand times just for good measure. When they’re ready to unleash the spam here’s the next trick.

When the spammer is good and ready they set up a realistic sounding post linking to them. It will show up in either technorati, or if they do a trackback it will actually show up as a comment as well. Stupidly, I’ll go and click on the link and end up at the spammer’s website. Ensuring that you only show the command to the right person can be done through IP delivery if you know their IP address, or using referring URLS. Embedded in the website is an invisible iframe with content that looks something like this:

[https://pastebin.com/6MMqD5hR](https://pastebin.com/6MMqD5hR)

While this isn’t particularly interesting from a web application security perspective it is interesting when you consider what it can be used for from the blackhat search engine optimization community. One of the things they are most interested in is persistant XSS, or rather links that will stay on the page indefinitely. While WordPress does add “rel=nofollow” to each tag, it doesn’t stop the actual text from being indexed. Splogging is not particularly effective due in parge part to the search engine’s respecting the rel=nofollow tag, as well as for moderation of comments (which we can now get around after the fact). Mitigating factors include deleting the content for good, and building better session/flow management.

From a web application security perspective things like changing the administrator password are vulnerable only if a referring URL can be spoofed (which is possible using the Flash header spoofing trick that Amit came up with). Because the state is dealt with by spoofable items (referring URLs) and CSRF susceptable tokens (cookies) WordPress is ultimately vulnerable to quite a bit more than just comment spam. (The same is true with submitting new posts, which by the way actually could enable XSS attacks as full HTML is allowed). So turn off Flash if you’re an blog administrator until something gets fixed.

---

WP 2.02 (and below) was awfully vulnerable to CSRF. An attacker was even able to change the blogâ€™s templates. As WP templates can contain php-code this may result in remote code inclusion. Yieks. Newer WP versions employ soild protection mechanisms against CSRF though.

If you have some time at hand, check out the discussions in the following mailing list threat, to see how clueless some developers are when it comes to CSRF: http://comox.textdrive.com/pipermail/wp-hackers/2006-April/005666.html

---

Well, might be a bit old post. :) But including Matt himmself does not saw/still see it. :( That idea with the MD5/SHA1 hash can be expanded with a salt (to slow-down but not prevent) brute-force attacks. This is surely also a little “security by obscurity”.

Okay, they have done something with KSES which kills images from unprivileged users but what about iframes?

Btw: I found a security leack in the Akismet plug-in when you are in the spam-queue. :( I hope the WP community will listen up and will not blame as “just-another-so-called-security-researcher”. I use salts here in my PHP app and CPR plug-in. :)
