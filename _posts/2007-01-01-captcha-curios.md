---
title: CAPTCHA Curiosity
layout: post
tags: captcha
---

Tim Tucker posted an interesting solution to some of the CAPTCHA solving stuff going around. He posted that to comment on his blog you must enter any data, as long as it’s incorrect. So as long as you don’t type in whatever you see and it is six characters long, it will be solved.

As the posted noted, this isn’t particularly good security, as a) it can be broken by anyone who views the site and knows that rule (therefore it’s not good against targeted attacks), and b) if it ever gains popularity it will become standard in splogging software. Still, it’s an interesting take on the same old problem of blog spam.

---

IMO, there are 2 ways to reducing comment spam:

1. Reduce the benefit. The easiest way to do that is to make make all links in untrusted comments “nofollow”. That should eliminate any SEO benefits associated with spamming.

2. Increase the cost. If CAPTCHA can be solved for $0.60/hour, it probably makes more sense to force the user’s computer to solve a CPU-intensive problem. Alexa sells CPU time on modern 3.6GHz machines for $1/hour. If a human CAPTCHA solver can average 1 CAPTCHAs every 2 secs, that’s $0.33/KiloCAPTCHA. If we instead force the user’s machine to do 5 CPU seconds of work, that’s $1.39/KiloCAPTCHA, more than 4 times as expensive.
