---
title: Hack Detection Methods in Online Games
layout: post
tags: games
---

## I - Introduction

As some of you are probably aware, a lot of game companies have recently been cracking down on "hackers". They've implemented the entire spectrum of userland detection mechanisms, ranging from the ridiculously simplistic to the incredibly complex. Over the course of the past few weeks, I have devoted a lot of time to trying to find a general solution to the problem of detection evasion. In some sense, it juxtaposes our position as hackers, with that of the game companies. To exploit a game you have to find only one flaw in their system whereas they have to design a system without any flaws. Similarly, when we hide ourselves from their detection code, all they have to do is spot a single mistake of ours, and it is us who are charged with devising and implementing the perfect system. The below article is my attempt at accomplishing this. It is by no means complete or perfect, but I'd like to think that it is a first step in that direction.

## II - Detection of loaded modules

For this purpose i'm going to assume we need to load a module into the target(as we do in the case of most game hacks or bots). We must recognize two distinct instances in which a rogue module could be detected. Upon injection and then the rest of the time.



Nearly every dll injection method involves calling LoadLibrary at some point or another. So a simple way to catch any modules you wish to detect is to hook LoadLibrary(or LdrLoadDll, or whichever other lower level native
API's).

This problem can be solved in one of two ways. The first and simplest being randomization of the modules name. Since a great many legitimate pieces of software inject dll's into every process on the system(Trillian, AIM, hotkey software, etc..) no reasonable detection system can use a "white list" design(detection that involves making sure only verified modules are loaded, and considering anything that isn't explicitly good, to be bad). So a blacklist must be used, which makes it so that randomized module nomenclature is a perfectly acceptable solution to this detection technique.

The other method, which I implemented is to use one other method of dll injection, which i've called "manual mapping". It seemed at first like a very daunting task to emulate the windows PE loader and make everything
work correctly, but it turns out that it's not really all that difficult. My ManualMap(appendix) code does just that. It could use a great many improvements, I know, and in fact I have my own private vastly improved
version, but it's only a proof of concept.

After a module is injected into a running process, it can be detected in two ways. The first is to scan the module list or call GetModuleHandle on modules that you consider "hacks". This is mitigated by unlinking your
module from the list using a tool like CloakDll(appendix). Or using something like ManualMap so the module is never linked in the first place. I think the second solution is a bit better, but they are more or less the same.

The second way of detecting modules after they've been injected is much more clever. It is to iterate through every page on the system(pages are aligned on 0x1000 bytes, so this is actually feasible), and check it for
offending code signatures. This problem can be countered by using a modified dll loader that randomizes the offset from the page boundaries where the real data actually starts. However, a better solution I think is
to create two new blank pages enclosing your module. And then use VirtualProtect to set the PAGE_GUARD flag on these two pages. The PAGE_GUARD flag will generate a one-shot exception whenever the memory is accessed. Using an unhandled exception filter, vectored exception handling, or a KiUserExceptionDispatcher hook(I recommend the latter), you can catch these exceptions. This will let you know when you are being scanned and allow you to do whatever you like to prevent the detection code from spotting your module.

## III - Hooks, Patches and CRC checks

To create any worthwhile hacks it is almost always necessary to modify the games code in some way. However, code modifications are all too easy to detect, and until now nobody has come up with a viable generalized solution to this problem. I'm afraid I can't claim to have completely solved it, but I have found a way to tame it a bit.

I've come up with a way to hook functions without modifying any code in the target process at all. The only drawback is that you can only simultaneously hook 4 functions. My method is to use the debug registers (i.e. hardware breakpoints). You can see my implementation of it in the CHook class in the appendix.

Now, debug registers can be detected quite easily. Anyone calling GetThreadContext with CONTEXT_DEBUG_REGISTERS will see them, any exception handlers will get a context structure that contains them, etc.. The solution to this is to hook NtGetContextThread, NtSetContextThread, and KiUserExceptionDispatcher. Of course, you'd have to use a patch hook for those. Since quite a few antivirus/anti-spam/firewall programs hook functions like these to help "improve overall system security", it would be unreasonable for a detection system to label you as a hacker based soley on
the presence of modified bytes in your system dll's. This means that you can hook up to 4 functions without fear of them being detected.

Even though they may not detect you based solely on the presence of those hooks in the system modules, they still do leave you open to one potential avenue of detection. Which is to locate your hooks in the system modules,
parse the jump patches and determine where they lead. A subsequent CRC of the hook procedure would be more than enough for a positive identification.

There are again, two solutions to this problem. One is to hook by using an int03 breakpoint instruction, and then catching exceptions(this is also implemented in my CHook class if you look hard enough, you'll spot it) and
redirecting them to the proper hook procedure. This would require you to either use a standard jmp patch hook on KiUserExceptionDispatcher(which would sort of defeat the purpose) or use one of the two standard forms of SEH.

The other solution which I consider much better, though slightly more difficult to implement is to write a polymorph engine for your hook procedures. It doesn't have to be anything too fancy, even randomized NOP-equivalent padding in-between actually relevant instructions(NOP equivalents are instructions such as mov eax, eax). This would make any
attempt at CRC checking your functions fail. I haven't yet implemented this method. However, I might end up writing some PoC code for it at some point.

The easiest method of doing this comes from the area of shellcoding. As i'm sure you all know, shellcode is often encrypted with a short runtime decrypting loader in order to evade IDS signatures. That runtime decryption stub is very easy to write a simple asm polymorph engine for. By simply placing NOP's in-between various instructions and using randomized encryption keys that change every time it is encrypted or decrypted, you could make it very difficult if not impossible to create any type of working signature for your code, without sacrificing too much in the way of performance.

The debug registers are also quite useful for many other interesting purposes. You can hook memory reads/writes as well as instruction fetches. This means you can create a callback for memory modification(great for values in memory you want to monitor, this means you don't have to poll them anymore). A complete description of them can be found in the appendix.

Another point to consider is that instead of attempting to detect your API hooks, they could simply disable them by patching over your hooks with the original bytes. This is easy to do and portable enough for a game company to consider implementing, since the first few bytes of most API's don't often change between versions of Windows. The solution to this problem requires us to realize that before being able to write to any memory in the code section of a process image, you'd have to call VirtualProtect to change it's page protection temporarily. So, a hook on NtProtectVirtualMemory should prevent them from simply overwriting all of your hard work.

## IV - Conclusion

In sum, it is possible to inject a module and set up to 4 completely undetectable(from ring3) hooks. There may be some holes in the specifics I presented, but the general theory i've described here can be applied to achieve that result. The above is my attempt at the most complete anti-detection system that can be created from userland. I'm sure you will
all be able to add your own insights onto what i've said, and I sincerely hope you do. The solution is not in secret security systems, like many of those currently involved in gamehacking seem to think...and as all closed source software vendors have found out. And game hackers above anyone else, should know that. Because you're all reverse engineers. You live to defeat security through obscurity...don't fall into the same trap yourselves.

## V - Appendix

ManualMap:
http://www.darawk.com/Code/ManualMap.cpp

Debug registers:
http://pdos.csail.mit.edu/6.828/2005/readings/i386/s12_02.htm

CloakDll:
http://www.darawk.com/Code/CloakDll.cpp

CHook:
http://www.darawk.com/Code/CHook.h
http://www.darawk.com/Code/CHook.cpp
