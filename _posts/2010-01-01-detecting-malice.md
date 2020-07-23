---
title: Detecting Malice With ModSecurity
layout: post
tags: security
---

[Ryan Barnett](https://web.archive.org/web/20150314222332/http://blog.modsecurity.org/2010/10/detecting-malice-with-modsecurity-geolocation-data.html) has a new series he’s doing called Detecting Malice with ModSecurity that I wanted to spend a minute talking about. Firstly, it’s personally interesting, because he’s using the book and slicing and dicing a lot of the core ideas and figuring out how to implement them. But secondly, I like practical examples of solutions to concepts that may seem to be unattainable or a technological hurdle at times. One of the reasons I didn’t spend any time talking about solutions was because so many people have varying platforms. That’s one of the nice things about the Internet but it’s also one of the problems. It seems like attacks are easier to talk about because nearly everyone is vulnerable to them. But defense is much harder, because it is always very site specific.

Anyway, it’s a great series and I recommend it, even after just the first post - not just because it’s talking about the book, but also because he really does a really nice job of giving thorough examples. I hope some people get some value out of it. Even if you use IIS, ideas like this get the creative juices flowing. Sometimes it’s tough being a security guy, so any little bit helps.

---

ah, i hate IIS, we use it here at work (despite my wishes we use APACHE and a linux or unix box)

i tried getting it to set a default page as “somepage.php?page=variable” but it wont allow those things, it has to be a document. so i had to make an html file that redirected to “somepage.php?page=variable” im pretty sure i could have easily done that with an htaccess file. not to mention permissions, mod_rewrite etc. the only thing IIS has going for it is a gui(which im not personally much of a fan of guis, advance things like managing a web site dont need guis, a gui is for simple tasks or people who dont know how to use a computer much. advanced tasks demand advance tools they need to be good, not easy)
