---
title: Mutli Threaded Digital Rights Management
layout: post
tags: drm
---

After Sony’s DRM rootkit fiasco, I started thinking about the concept of threaded digital rights management. The concept is simple enough. Let’s say you have two computer programs. One is installed and working fine. Then a year or so later, you install a second one, and then suddenly the first one completely stops working. These forms of software conflicts have happened to all of us at one point or another, but what if it could be used for digital rights management?

What if you had two pirated computer software programs. One that is the “victim”, and one that is the “killer1″. The victim gets pirated (because it’s old software and already out there). Then sometime later, the killer1 software gets installed and then sees that the victim software is installed and immediately cripples it in a way that the victim software writer would have wanted their software to be crippled. The two software packages don’t even have to know anything about eachother, they just have to agree on a course of action if they see signatures that the other software provider would want crippled.

Then you have victim software, which is crippled, and killer1 which has disabled it. They may then pirate or otherwise crack the killer software but then sometime down the road they download killer2 software. Killer2 sees a cracked version of victim and killer1. Killer2 disables killer1 in a way that the authers of killer1 would have wanted a pirated version to be crippled, and indeed cripples the original victim software if the cracker found a way to uncripple it. And so on… Software protecting software. Now this is making an assumption that the user would even know what’s going on. Typically it is easy to disable the copywrite protection on software, but it could be exponentially more difficult to remove software like this if it were coded properly, because you have to know exactly what it is looking for and disable it or hide it from the process as it installs.

Software that defended itself could be very tricky to disable, as I said, but it could take weeks or months to even realize which software found and disabled which other software if it is not a highly used application. Additionally it would be very easy to get some freeware application that everyone used (think Winzip or Winamp) to embed something like this after their userbase was large enough. Once the DRM software was in place it could wipe out huge swaths of pirated software from working.

I know that Microsoft has been working feverishly on thier embedded DRM software which has had a number of bugs, for sure, and I think this would have the same problems that Microsoft has seen, but the premise might just prove to be a powerful tool for software intellectual propery owners. Threading it, or distributing the problem, might serve better than any one software company trying to protect themselves.
