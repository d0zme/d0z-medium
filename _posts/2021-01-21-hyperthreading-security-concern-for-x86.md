---
title: Is Hyper-Threading a Security Concern for X86 Servers? OpenBSD Devs Believe So.
layout: post
image: https://i.imgur.com/dK230CG.gif
permalink: /hyper-threading-security-concern-openbsd
---

Hyper-threading has been a feature in many Intel processors since the Pentium 4 HT days. Unfortunately, security experts are coming to the conclusion that hyper-threading exposes data to potential attacks between processor cores, which is especially dangerous to web servers hosting multiple websites. This is the justification to why the [OpenBSD development team have disabled hyper-threading](https://www.mail-archive.com/source-changes@openbsd.org/msg99141.html) in the latest x86 releases.


Having multiple threads in one processor core, also known as Simultaneous Multi-Threading, will usually share memory caches between threads. This only adds additional vectors to speculative execution attacks (like Spectre) and could be used to compromise data on shared servers.

Since Intel now has a habit of forcing hyper-threading on modern platforms, it is a difficult task to disable it from the operating system. OpenBSD is using their processor scheduler to disable hyper-threading when used on their Amd64 kernel. They also plan on extending this exclusion to other manufacturers and architectures, so it is not an attack directed at Intel.

## Will Hyper-threading Be Missed?

Intel chips with hyper-threading shine when they are used to render videos or images, mining cryptocurrencies with multiple threads, or running lots of background processes. The technology allows for one core to work on processes in parallel but not as adding an additional core. Some people may be confused by this fact since their task manager shows double the amount of processors.

While SMT does have its benefits when a processor is under a very heavy workload, it is not always the case for real-world applications. A typical end user on their workstation computer may not even notice a difference in daily usage when limited to one thread per core.
