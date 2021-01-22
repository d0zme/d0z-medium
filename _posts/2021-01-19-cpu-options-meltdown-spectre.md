---
title: What Are My CPU Options to Avoid Spectre and Meltdown?
layout: post
image: https://i.imgur.com/EWVK2yW.jpg
permalink: /cpu-options-spectre-meltdown
---

Spectre and Meltdown are code names given to published exploits showing major security flaws in processors made within the past 20 years. These exploits are possible on any x86 processor with out-of-order execution, which affects nearly every Intel processor on the market (with few exceptions like Atoms).

Thanks to the fact of the speculative (or out-of-order) execution having access to memory prior to receiving permission, this leaves protected memory wide open. With this exploit, hackers are able to gain access to data found within a processor's cache with the possibility of uncovering passwords and other secret data. Theoretically, it could even be launched with JavaScript through a user's web browser.

Those that have servers or workstations with precious data are likely worried about such exploits and considering a switch from Intel to more obscure hardware architectures. While the options are limited due to the traction that Intel has in the computing market, there are some possibilities to consider.

## Avoid Windows

Let's face the fact that Windows has the high risk of local or remote exploits, regardless if the user is using a vulnerable processor. Hackers only need one small loophole to execute their Spectre or Meltdown derived code to gain access to essential operating system components.

The Linux kernel, FreeBSD, and OpenBSD were one of the first responders to make sure that their x86 operating systems were resistant against this new exploit. You may be significantly safer on x86 using these operating systems with stable user-level programs than with Windows.

## Switching to POWER ISA Processors

Power ISA processors are not vulnerable to the Intel-specific Meltdown exploit but can technically be attacked by Spectre-like exploits. The issue an attacker will have with POWER processors, especially older ones, is that it would have to be specific to the processor architecture. Such exploits would also run very slowly on older Power Macs, making an attack even less practical. A Power Mac with a G5 processor may have the most exposure to speculative execution attacks since it is the most efficient within the Power Mac line in that regard.

Using a PowerPC machine is doable with even old systems, but that depends on your computing needs. For instance, an iMac G5 can run most modern programs if used with an up-to-date Linux or BSD operating system. With Newer IBM machines, AIX is still being updated and even have patches to thwart potential Spectre-like CPU exploits.

Some PowerPC Products include:
- Macintosh computers with G3, G4 & G5 processors. 
- Raptor Computing Talos II with POWER9 processors 
- IBM Power servers and workstations. Power7+ and forward receive official firmware updates. 

## Switching to ARM

Due to its popularity in mobile and embedded devices in recent years, there are many ARM processors on the market to be evaluated. All the way from the original iPhone to the Raspberry Pi, this architecture is found everywhere and each processor may have an original set of features.

You can forget about Meltdown being a risk to any ARM processor since it is Intel specific. As the official document released by ARM (developer.arm.com/support/arm-security-updates/speculative-processor-vulnerability) points out, there is a potential threat from Spectre variants in Cortex processors.

Since most ARM products are used in closed environments, only the "A" class of Cortex processors have real-world exposure. For example, the Cortex-A76 is vulnerable to Variant 1 and Variant 2 of Spectre while immune to the rest.

Although intended for phones & embedded applications, ARM processors may certainly be viable as a desktop/server replacement in the near future. Quad core CPU boards, like the Raspberry Pi 3 or ODROID devices, are able to run a lot of servers, workstation, and gaming applications. The Cortex-A76 processor intends to compete against mobile Intel i5 processors while using less than 5W of power.

## Switching to SPARC

Since processor memory management is handled completely differently than x86, SPARC is immune to meltdown and some variants of Spectre. Oracle even released a statement that they believe meltdown will not be an issue on SparcV9 processors.

Starting with the S3 core, there are later releases of SPARC that do have speculative execution built-in. This does leave the possibility that SPARC could be attacked by Spectre variants in the future, which is why Oracle continues to release microcode patches.

Since the workstation market of SPARC was demolished by Windows & Intel with the release of Windows 2000, the modern market is server based. It may possible to install graphics cards in some SPARC servers, along with generic Xorg drivers, to make a usable workstation. Sun's old workstations are too slow to be considered for modern computing, although installing Linux or NetBSD may bring some life back into them.

Some modern SPARC servers to consider:
- UltraSPARC T1 - This includes the Fujitsu Siemens T1000 and T2000, Sun Fire T1000, and Sun Netra T2000 Server, 
- UltraSPARC T2 - This includes the Fujitsu Siemens T5120 and T5220, Sun Blade T6320, and Sun Netra CP3260. 
- Oracle SPARC T3-T5 
- Oracle SPARC M7-8 

## Switching to RISC-V

RISC-V is an open source architecture that is open for the world to design and release processors. It was released by UC Berkeley in 2010 but there haven't been real-world applications up until the past couple of years.

Since no current RISC-V processor accesses memory speculatively, the ISA is considered to be immune to Meltdown or variants of Spectre. Of course, that does not mean that future RISC-V producers won't choose to implement speculative execution.

Commercial availability of RISC-V is still quite limited but things are looking promising. SiFive produces a quad-core RISC-V SOC that may be comparable to a Raspberry Pi. Imperas, Codasip, and GreenWaves Technologies also have some IoT and embedded products. We should also expect more developments to come from NVIDIA, Western Digital, ETH Zurich, and Esperanto Technologies. Thanks to the Computer Laboratory from the University of Cambridge, FreeBSD had been successfully ported to RISC-V.

## Coreboot & Libreboot for x86 Hardware

Unfortunately, most outdated motherboards lack BIOS updates that may defend against Spectre, Meltdown, or future processor exploits. Fortunately, Coreboot is laying down the groundwork to replace x86 motherboard BIOS firmware with a faster and more secure operating system with a robust Linux kernel.

Coreboot support ranges from Pentium 1 processors to some Sandbridge-Based processors from 2013. There are a handful of boards that are easily flashed from a command line utility within Linux, while many others require external programming devices to flash. Before considering replacing your default firmware, check to see if essential features are missing in each motherboard's manual page on Coreboot's website.

Libreboot is a more extreme version of Coreboot, in which all binary blobs have been removed so that there is not a shred of non-free code within the firmware. This may qualm the extra paranoid but it also limits our options to just a few older motherboards. Supported hardware includes Thinkpads x60 & T60, Macbook 1,1 & 2,1, and a few AMD server motherboards.

While having either Coreboot or Libreboot does not offer complete protection from exploits against out-of-order execution exploits, having an up-to-date Linux kernel as a part of the firmware plus a non-Windows operating system does mitigate the threat.

## Conclusion

With a long lineage of x86 processors being affected, this may be the best opportunity for the CPU market to diversify in decades. Intel also has a bad track record of privacy and security since a Minix-based web server was discovered on processors that include the Intel Management Engine. Hopefully, Intel and future leading processor manufacturers will make security a priority over performance.
