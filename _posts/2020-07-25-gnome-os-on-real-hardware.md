---
title: GNOME proposes bringing GNOME OS to real hardware
layout: post
permalink: /gnome-os-on-real-hardware
image: https://i.imgur.com/93QhpLq.jpg
--- 

At the **GUADEC 2020 conference**, a report was made on the development of the "GNOME OS" project in which a plan is released to develop "GNOME OS" as a platform for creating OS now transformed into consideration as a set that can be used for continuous integration, simplify working applications in tests developed for the next version of the GNOME code base, development assessment, hardware compatibility testing and user interface experimentation.

It should be remembered that the GNOME OS build initiative came about in 2012 in order to address issues in GNOME development and also to offer several ideas for increasing demand for the platform.

Until now, all GNOME OS compilations have been designed to run in virtual machines.

[And now with the new initiative, it is intended that the work that has been done now will ensure that GNOME OS is used on real hardware.](https://events.gnome.org/event/1/contributions/80/attachments/7/14/gnomeos-hardware-guadec2020-handout.pdf)

This means that new compilations are being developed for x86_64 and ARM systems (Pinebook Pro, Rock 64, Raspberry Pi 4). Compared to the compilations for virtual machines, the ability to boot into systems with UEFI, power management tools, print support, Bluetooth, WiFi, sound cards, microphone, touch screens, graphics cards and webcams was added, as well as the missing Flatpak portals for GTK+. Flatpak packages prepared for application development (GNOME Builder + SDK).

To form the system that completes the GNOME operating system, the OSTree system is used (the system image is atomically updated from a repository similar to Git), by analogy with the Fedora Silverblue and Endless OS projects.

Initialization is done with Systemd. The graphical environment is based on the Mesa, Wayland, and XWayland drivers. We suggest using Flatpak to install additional applications, while the installer is the Endless OS installer based on the initial configuration of GNOME.

## Gnome is committed to the environment

Another issue addressed at GUADEC 2020 was a proposal to consider the environmental impact of developing GNOME applications. For each application, it is suggested to show a "Carbon cost" parameter, which shows the approximate level of carbon dioxide emissions to the atmosphere, allowing to evaluate how the development affects global warming.

According to the speaker, although the free software is provided for free, it has an indirect price: the impact of development on the environment.

> For example, a project's server infrastructure, continuous integration servers, GNOME Foundation and developer conferences all require electricity and materials that emit carbon dioxide from manufacturing processes. Applications also consume energy in the user's systems, which also indirectly affects the environment.

The introduction of the new metric will show that the GNOME Project is serious about preserving the environment.

The factors for calculating the k-metric are application runtime, CPU, storage and network load, and the intensity of testing on the continuous integration system.

To evaluate the load, it is proposed to use sysprof, systemd and powertop accounting mechanisms, whose data can be converted to the equivalent of carbon dioxide emissions.

> For example, 1 hour of CPU-intensive loading can be estimated as approximately 20 W or 6 grams of CO2e, and 1 GB of data downloaded from the network as 17 grams of CO2e. With respect to continuously integrated systems, the Glib array is estimated at 48 kilograms of CO2e per year (in comparison, one person produces 4.1 tons of CO2e per year).

To reduce the cost of carbon, developers are encouraged to implement optimizations such as caching, improve code efficiency, reduce network load, and apply pre-defined images in a continuous integration system, thus contributing to the fight against global warming.

For example, using ready-to-use docked images in a continuous integration system will reduce the value of the metric by 4 times.

For each major release, it is suggested to calculate a Cumulative Carbon Cost that summarises the metrics for all applications, plus the costs of the GNOME Project, GNOME Foundation, Hackfests and Continuous Integration.

Such metrics will allow development to be carried out taking into account the impact on the environment, to track the dynamics and to carry out appropriate optimizations.
