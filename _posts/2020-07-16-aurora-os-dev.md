---
title: Aurora OS developers included a memcpy fix in Glibc
layout: post
tags: mobile
permalink: /aurora-os-developers-included-memcpy-fix-in-glibc/
image: https://i.imgur.com/VeO8EMR.png
---

The developers of the AuroraOS mobile operating system (a fork of the Sailfish operating system, developed by the Open Mobile Platform company) shared a solution for a vulnerability they detected in memcpy. The removal of the critical vulnerability ([CVE-2020-6096](https://talosintelligence.com/vulnerability_reports/TALOS-2020-1019)) in Glibc, which manifests itself only in the ARMv7 platform.

Information about the vulnerability was disclosed in May, but until the last few days, fixes were not available, despite the vulnerability being assigned a high level of danger and there being a working prototype of the exploit to organize code execution.

The prepared exploit acts during processing on the memcpy() and memmove() functions for certain formatted data.

The importance of Glibc is that this library defines system calls and other basic functions and is used by almost all programs.

## About the problem

The vulnerability was manifested in the implementation of memcpy() and memmove() in assembly language for ARMv7 and was caused by incorrect processing of the negative values of the parameter that determines the size of the area.

Problems with patch development began when SUSE and Red Hat announced that their platforms were not affected by the problem, as they did not form builds for 32-bit ARMv7 systems and were not involved in creating the patch.

The developers of many embedded distributions apparently trusted the Glibc team, and also did not take an active part in preparing the patch.

## Solutions

Huawei offered an option for a patch to block the problem almost immediately, which sought to replace the assembler's instructions operating on signed operands (bge and blt) with unsigned analogs (blo and bhs).

Glibc maintainers developed a test suite to test different conditions for the occurrence of an error, after which it turned out that Huawei's patch does not fit and does not process all possible combinations of input data.

Since AuroraOS has a 32-bit compilation for ARM, its developers decided to close the vulnerability on their own and propose a solution to the community.

The difficulty was that, it was necessary to write an effective assembler implementation of the function and consider several options for the input arguments.

The implementation has been rewritten using unsigned instructions. The patch turned out to be small, but the main problem was to maintain execution speed and eliminate performance degradation of the memcpy and memmove functions, while maintaining compatibility with all input value combinations.

In early June, two solutions were prepared, passing the Glibc maintenance test framework and Aurora's internal test suite. On June 3, one of the options was selected and sent to the Glibc mailing list.

A week later, another similar approach was proposed, which solved the problem in the multiarch implementation, which Huawei had previously tried to solve. A month took testing and legalization in view of the importance of the patch.

On July 8, corrections were accepted in the main branch of the next glibc 2.32 release. The application includes two patches:

- The first for a Multiarch memory setting application for ARMv7
- The second for a common assembler implementation of memcpy () and memmove () for ARM.

The problem affects millions of ARMv7 Linux devices and without a proper upgrade, owners risk connecting them to the network (services and applications available on the network that accept input without size restrictions can be attacked).

For example, an exploit prepared by researchers who discovered the vulnerability shows how to attack an http server embedded in the car information system by transmitting a very large GET request and gaining root access to the system.

The package solutions for Debian and Ubuntu have not yet been released and the vulnerability remains unfixed for almost two months from the time of public release and five months from the time Glibc developers were notified.
