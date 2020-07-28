---
title: Tip to make your Raspberry Pi 4 Much Faster
layout: post
image: https://i.imgur.com/3pOoU94.jpg
tags: hardware
---

If you want your **Raspberry Pi 4** to perform at its best, this trick will help you get the most out of it when using USB storage devices.

Over the past few weeks, the **Raspberry Pi Foundation** has been testing their new USB firmware on Raspberry Pi 4. This serves to make the board capable of booting and storing data from a USB more stable and faster. Still, it is not the fastest system we can use. 

Many users like Jeff Geerling are wondering how to make their Raspberry Pi go faster. To find an answer, Geerling has posted the results of several tests [he has conducted on his blog](https://www.jeffgeerling.com/blog/2020/uasp-makes-raspberry-pi-4-disk-io-50-faster). He has examined the speed Raspberry Pi 4 achieves with different USB 3.0, microSD, or USAP storage solutions. 

According to Geerling's tests, a USB 3.0 SSD is ten times faster than the fastest microSD card he tested. However, this is not the fastest system we can find, a comment from another user put Geerling on track: he had not tested the UASP (USB Attached SCSI) system. 

UASP or UAS stands for USB Attached SCSI (UAS) or USB Attached SCSI Protocol (UASP). This is a computer protocol used to move data with USB storage devices such as hard disks (HDDs), solid state drives (SSDs), and USB memory drives.  This protocol generally allows faster transfers compared to the BOT, Bulk-Only Transport.

BOT was designed to transfer files when the fastest speed a USB could get was 12 Mbps. According to Geerling, tests show a BOT transfer rate of 172.13MB/s, but if we use UASP the transfer rate goes up to 296.71MB/s.

After these tests, the results show that it is advisable to always use USAP with USB 3.0 devices to achieve higher transfer rates with our Raspberry Pi. It's important to remember that USB 3.0 must be plugged into the blue USB 3.0 ports and not the black USB 2.0 ports, otherwise we won't gain any performance.
