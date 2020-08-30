---
title: Proposal to modify Mesa so that NVIDIA can run applications with XWayland
layout: post
image: https://i.imgur.com/ljEDUOi.jpg
---

NVIDIA has always demanded special treatment within the Linux ecosystem, an attitude that caused Linus Torvalds himself to explode a few years ago. The creator of the kernel sent what is probably the most beloved hardware company in the PC gaming industry on a very rough ride.

Far from changing its attitude, NVIDIA continues its pulse against the standards agreed upon by all but it. In an article titled "Some Ugly Code Can Make NVIDIA's Linux Driver Work with Accelerated XWayland," the [Phoronix media](https://www.phoronix.com/scan.php?page=news_item&px=GLX-Delay-Accel-NV-XWayland) exposes that a Red Hat developer has been working on a feature called GLX Delay.

Basically, the purpose of GLX Delay is to make the NVIDIA Linux driver capable of supporting accelerated GLX with XWayland, the Xorg implementation for applications that do not natively support Wayland. According to Phoronix, "The proposed code is going through Mesa even though it is for the benefit of NVIDIA's proprietary driver and also requires a change in the OpenGL Vendor Neutral Dispatch Library (libglvnd).

As we said in the opinion article, NVIDIA requires custom configurations and modifications for its driver to work properly with Wayland, and here is an example. This development aims to make 'glxgears' and 'glxinfo' run correctly on XWayland with the official NVIDIA driver. According to Adam Jackson, the Red Hat developer who has proposed GLX Delay, the applied approach should allow the rendering of GL to be as fast as in Xorg and EGL, which in theory should bring, for example, great benefits when running games on XWayland, something that AMD users have been able to do for some time.

In short, within not much NVIDIA users should have the basis for running video games on Linux from a Wayland session, however, there are still many features to implement, such as resizing windows on XWayland, several features of GLX, additional features of SwapBuffers that are not connected as vertical synchronization and more things. The proposed changes to Mesa are basically dedicated to reusing GLX's own code.

Adam Jackson has defended his work by saying that "I want the xfree86 code out of my life, and this approach seems to eliminate a big class of reasons why you might need to use Xorg and the NVIDIA driver. It's certainly better than what's currently available to GLX clients in that scenario, which is llvmpipe. On the other hand, I can see the argument that this strengthens the position of NVIDIA's libEGL, as we have made it more usable. But I think, at the end of the day, this reduces the footprint of the binary driver, and I think that's a good direction to go in.

It is curious that in order to accommodate NVIDIA in Wayland, Mesa has to be modified, a component that does not appear in the minimum requirements for installing the proprietary driver and that does not need to be updated in that context. We'll see how the matter evolves, but everything points to more "ugly code" in the future so that NVIDIA can function correctly in Wayland.
