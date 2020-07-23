---
title: FireSheep Reviews
layout: post
tags: network
---

I go back and forth on whether I think FireSheep is interesting or not. Clearly, it’s old technology re-hashed. But it is interesting not because it works, but that it surprises people that it works. We’ve been talking about these problems forever, and now companies are scrambling to protect themselves. I guess the threat isn’t real until every newbie on earth has access to the hacking tools to exploit it.

One of the more interesting analysis pages I’ve seen was one which had a scorecard. At first blush it’s fairly obvious but one thing stuck out at me regarding the last part of the scorecard, where they assigned scores to each of the various protocols like POP3 fails but POP3 over SSL/TLS gets an A. The interesting thing is that there isn’t an equivalent score for HTTP vs HTTPS. This all goes back to the 24 vulnerabilities Josh and I talked about in the browser implementation of SSL/TLS in the browser.

Just because something is speaking HTTPS some of the time doesn’t even mean that session alone is secure in a multi-tabbed environment, or with certain plugins, or certain settings or with certain settings within cookies, etc… It’s just not that straight forward. Wouldn’t it be nice if we had something that did act in a safe and sane way that allowed you to contact a site securely? Maybe something that was a secured transport layer (no, not TLS, I mean something actually secure). ;) Maybe it’s something we can add on top of SSL/TLS over DNSSEC while we’re in the browser security world are still in the mood to shake things up.

---

It’s all about making something theoretical into something practical that you can see and feel. People don’t get very scared over “theoretical threats”. That’s why when the media tries to scare you they always start with a narrative about an individual that they hope you can relate to. That’s also why people frequently ignore pen test reports unless the tester can go the extra step and really demonstrate in clear and obvious terms not what COULD be done, but rather what HAS been done. (You’ve never seen an IT team scramble as fast as when you physically deliver them their customer’s PII stolen from their systems).

---

I tried firesheep a few weeks ago and I couldn’t get it to work. My wifi network is unsecure but maybe there is some other layer of encryption on my router (netgear). I had one computer on firefox listening and I used another computer to browse twitter and facebook in both Safari and IE. I couldn’t snag anything. I’m sure I could test a few other scenarios with my machines but if I couldn’t easily grab something on my own network, then I don’t think I would go to the local starbucks to try anything. Seems like the tool has potential though if it works. Angel One is correct, people don’t pay attention until the carpet is pulled out from under them.

---

Firesheep is interesting not for what it does, but for how easy it makes the task. Now that the process of stealing session cookies has been simplified to a one-click addon that any idiot can use, people realize that this vulnerability exists and just how severe it is.

---

