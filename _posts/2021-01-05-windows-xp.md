---
title: Making Windows XP Usable in 2021
layout: post
image: /images/xp.jpg
permalink: /windows-xp-guide/
---

Windows XP is long dead in the eyes of Microsoft, and anyone still using it is on their own to secure their own systems and find programs still available for modern computing.

With that said, it's still a fun operating system to tinker around with, and for very old computers, it may perform better than Windows 7 or Linux.

Here is a mini-guide I wrote for those still wanting to do modern stuff on their old machines without having to upgrade to an undesirable operating system.

*Note: If you are looking to obtain Windows XP for free, Microsoft still has Windows XP-based POSREADY 2009 edition that's freely available to download.*

## Networking

While Windows XP was left in the dust, it's network stack is still perfectly fine to connect to modern network infrastructure. There are a few handy tools I would install to enhance the security and integrity of your system.

### Security

**Netlimiter** is the best traffic monitoring program I've found for Windows. You can limit/block connections to certain programs, monitor where traffic is going at a system-wide level. **NetLimiter 3** is the last release that supports Windows XP, and it comes in both paid & freeware versions.

### VPN

The last version of OpenVPN to support XP is [2.3.18](https://github.com/OpenVPN/openvpn/releases/tag/v2.3.18), and proprietary programs from VPN providers are unlikely to work on Windows XP out of the box. I would recommend installing the last version released, and manually run OpenVPN with configuration files from your provider (if available).

### Using Programs With Proxies

If you need to access the internet using a local proxy (such as at a university), you'll notice lots of old programs outside of your web browser do not offer proxy settings.

This is where **SocksCap** comes in handy. Much like proxychains in unix-like operating systems, you can chan proxies in order to get just about any program work tunnel through a socks proxy (including Tor).

For an open-source implementation, be sure to also check out FreeCap hosted on Github.

### Mobile Tethering

If you are out of luck finding a Wifi or ethernet driver to work on the operating system, you may consider connecting via USB tethering on your mobile phone. You can either use mobile data from your carrier, or connect to your WiFi router and pass it through via USB tethering.

I would highly recommend installing PDANET for two reasons:
- It automatically installs the ADB Driver to get your phone working with the operating system.
- It can be used to bypass tethering limits if you are on a budget phone plan. (Be sure to check out [my other article about PDANET](https://d0z.me/pdanet-on-linux-freebsd-unix)...).

## Web Browsing

Whatever you do, do not touch Internet Explorer. In fact, it's possible to disable it by going to the **Control Panel** -> **Add or Remove Programs** -> **Set Program Access and Defaults** -> **Custom** -> **Choose a default Web browser** -> **Clear the Enable access to this program button**

To remove security vectors, it's ideal to browse most websites without Javascript or any plugins. This is why I would have at least two web browsers installed for security purposes.

### JavaScript-Free Web

[NetSurf](http://www.netsurf-browser.org/downloads/windows/) is the most basic, open-source web browser you can find, and it's available for just about any operating system. It's intended to browse the internet with bare-minimum, resources, and if you turn off Javascript rendering, you will browse the internet with static HTML pages.

![](https://upload.wikimedia.org/wikipedia/commons/3/32/NetSurf.png)

### Fully-featured Web Browsing

Java and Flash have been axed long ago, so having a web browser that's up-to-date with HTML, Javascript, and security certificates should make web sites programmed with modern techniques usable.

[MyPal]() seems to be the most popular browser by XP enthusiasts. It's based on Mozilla Firefox (meaning you can install add-ons) and the project aims to be the most functional browser available for Windows XP.

![MyPal for Windows XP](https://archive.vn/g6ODV/3206e21b3f1e3e5ff57a5e297b36bed6e8c871a4.png)

**Otter Browser** is another browser you may experiment with if you needs are quite minimal. The browser tries to emulate the user experience of Opera 12, and is built on the QT 5 platform. While it's more geared towards Linux users, [they still support Windows XP in the latest builds](https://sourceforge.net/projects/otter-browser/files/otter-browser-weekly360/otter-browser-win32-weekly360-xp.zip/download).

![Otter Browser Preview](https://camo.githubusercontent.com/006862e12a1ef640aea29d6564077fd2a0d0b1729f5af8097a97fe406abdc249/68747470733a2f2f6f747465722d62726f777365722e6f72672f73637265656e73686f74732f312e706e67)

## Gaming

Windows XP is the ultimate operating system if you want to load up your original discs of games made during the Golden Era of PC Gaming. I had no problem firing up any of the Command & Conquer games up to Red Alert 3, Warcraft 3, Starcraft, and OpenArena during a test run.

Getting into DRM territory with modern games is when it gets tricky. Steam stopped making builds for Windows XP in 2019, so people have to install older versions or come up with workaround to get certains games to work. [This guide at the MSFN board](https://msfn.org/board/topic/178386-guide-run-steam-on-windows-xp-and-vista-in-2019/) is worth a read.

## Virtual Machines

Using Windows XP as a hypervisor to run modern operating systems is quite silly, but still, it's entirely possible to run just about anything you need in Virtual Box. You may have to [dig around in their archives](https://www.virtualbox.org/wiki/Download_Old_Builds) to find a build supported on your machine.

To emulate other processor architectures, it is possible to build [QEMU](https://www.qemu.org/download/) for Windows XP.

[PearPC](https://sourceforge.net/projects/pearpc/) is a classic emulator if you wish to create PowerPC Mac virtual machines. 

## Conclusion

Windows XP is still usable, even though it's now far beyond the reach of security updates, so you must always be vigilant in how you use your computer.

To be sincere, you are better off using Windows XP within a virtual machine, and/or completely disconnected from the internet.
