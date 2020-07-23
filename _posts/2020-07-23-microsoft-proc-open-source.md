---
title: Microsoft releases Procmon for Linux as open source
tags: microsoft
image: https://i.imgur.com/f8wkUrl.jpg
permalink: /Microsoft-releases-Procmon-for-Linux-as-open-source
---

Microsoft continues to demonstrate its "love" for Linux by [releasing more components that end up in the Open Source system](https://github.com/microsoft/procdump-for-linux). The Redmond giant has released quite a few components throughout this decade (2011-2020), including Visual Studio Code and the .NET server part, as well as publishing the exFAT specifications and publishing Open R under GPLv2. Now it's Procmon's turn, one of Sysinternals' tools.

The arrival of at least some of the Sysinternals tools to GNU/Linux is not new, since Microsoft announced its intentions in that sense two years ago. After porting ProcDump, it is now Procmon's turn, although its version for GNU/Linux has some important differences from Windows.

## Procmon for Windows

Sysinternals is a set of free tools that allow you to obtain detailed information about the operating system and to monitor it. Although it was born as an independent development, in 2006 it ended up being acquired by Microsoft, which has since then maintained, developed and improved it until today. Focusing on Procmon, the company explained in the GitHub repository dedicated to this software that "Process Monitor (Procmon) is a Linux reinvention of the classic Procmon tool from the Sysinternals toolkit for Windows. Procmon provides a convenient and efficient way for Linux developers to track syscall activity on the system.

In short, this is not a conversion of the tool available for Windows, but something reprogrammed from the base. This makes sense considering that GNU/Linux is a radically different operating system from Windows, so, unless the intention was to make it work in Wine, which it is not, it was necessary to reprogram the core parts of the tool again, a process that at least for the moment has taken away the graphic interface (quite retro in the Windows version as you can see in the image).

## Procmon for Linux

Microsoft has asked for collaboration in order to obtain feedback to improve the Linux version of Procmon, which like ProcDump is published in GitHub under the MIT license. For now the installation is done by compilation and asks for Ubuntu 18.04 LTS as operating system with a kernel between versions 4.18 and 5.3 together with cmake 3.13 or later and libsqlite3-dev 3.22 or later, plus other dependencies.
