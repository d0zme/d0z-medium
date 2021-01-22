---
title: What is MINIX and Why is It Included in the Intel Management Engine?
layout: post
image: https://i.imgur.com/uHu0wlz.png
permalink: /minix-intel-me
---

The Intel Management Engine has been a motherboard component that had remained under the radar in until recent years. Since 2008, it was available to most motherboards as a removable chip and had the possibility of being disabled. Motherboards that are produced in 2016 and beyond will have ME integrated within the Northbridge, meaning it cannot be removed.

This component features a modified version of the MINIX 3 operating system running a discreet web server. MINIX will remain running when your computer boots up, is put to sleep, or even when running your operating system. It's like an embedded computer within your computer, as it even has its own processor, memory, and storage.

Not surprisingly, the general public is starting to question their security and privacy with such an intricate subsystem running without their permission. MINIX is also receiving more attention than ever since we now know of its presence in most x86 desktop and server computers.

## What is MINIX?

MINIX is the creation of Andrew Tanenbaum with the intention of teaching operating system design and was sold along with its respective textbook. Prior to Linux, which was inspired by MINIX, this was a go-to operating system within the academic community. For modern uses of the operating system, it is used in critical environments that have extremely limited computing resources.

MINIX is a micro-kernel operating system, as opposed to the monolithic kernels used in Linux or FreeBSD. While having a micro-kernel comes at a loss in performance, it is nearly immune to crashes since most drivers and processes are in the user space.  In comparison to Linux or any BSD operating system, it is indeed one of the most secure options. This doesn't mean that exploits cannot be developed for the operating system.

## Security Concerns for the Intel Management Engine

For those that are not familiar with protection rings, it prevents certain applications having access to different levels of processor instructions. For security reasons, higher level rings won't have access to lower level rings, but lower level rings can have access to the processor space above.

This embedded MINIX variant runs in Ring -3, which is the lowest level in protection rings that software can go. An operating system may typically utilize rings 0 and 1, meaning that it is much higher than the level of the Intel Management Engine. If this subsystem is compromised, your entire system is compromised.

Since the ME has internet connectivity, a remote hacker may access otherwise protect ed data and execute any root-level commands within your helpless operating system. Even scarier, unauthorized access extends into any network interfaces, RAM, and built-in cryptographic engines.

## Final Thoughts

In combination with the intrusive nature of the ME and other recent processor exploits (like Spectre & Meltdown), users are tempted to migrate towards AMD and other processor architectures. With ARM catching up in performance, RISC-V becoming commercial, and Talos II  resurrecting the POWER ISA for desktops, Intel may not have dominance in the desktop market in the near future. On the other hand, if the Intel ME proves to be rock solid against exploit attempts, this could only mean good things for MINIX in the embedded device market.
