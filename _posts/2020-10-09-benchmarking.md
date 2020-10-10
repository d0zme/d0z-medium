---
title: Benchmarking Your Computer on Linux
layout: post
image: https://i.imgur.com/fek6K8n.jpg
permalink: /benchmarking-linux
---

For anyone with a powerful gaming rig or server, benchmarking is one of the first things you do. There is a plethora of popular software available for Windows. Having said that, there are programs to test Hardware performance on Linux, BSD or Unix.

## Benchmark on Linux

I start with computers with Linux-based operating systems. There are two branches as Linux computers may or may not have a graphical interface. The everyday computer usually has it and the servers usually don't have it installed.

The program I recommend if you have a graphical interface is called **Hardinfo**.

To install it changes depending on the operating system. In Ubuntu and Debian simply update the repositories and install it. We can search on the official website how to install it for other distributions.

<pre>
sudo apt update && sudo apt install hardinfo -y
</pre>


All that remains is to go to the menu of our applications, search for Hardinfo and click on the icon to start it. Once opened it will show us first the system information. And if we continue downloading we have a section called Benchmarks. At the top we have a button called Reports. When you press it and select the section of Benchmarks it will execute all of them at once and save them in an html format.

![](https://i.imgur.com/fU4m6Gt.jpg)

## CLI CPU Benchmarking

Now for Linux but without a graphical interface, the most common in servers. You can also use these on a Linux with a graphical interface as they run from the terminal. I usually use it even if it has an interface because it is more comfortable.

The utility in question is called S-tui. To use it first we need Python and Stress to be able to run it and do the tests. As always, we can go to the official page to see how it installs in other distributions since it does have compatibility.

<pre>
sudo apt install python python-pip stress -y
sudo pip install s-tui
</pre>

Once installed, all that is left to do is to run it.

<pre>
sudo s-tui
</pre>

As soon as we run it we can see that although it is a terminal utility it is not simple text. We can go moving through the options and modifying it by pressing ENTER and ESC. We have two modes, the single monitor and the one that makes the CPU stress tests.

## Geekbench

Finally, we have a utility that can be used both as an application and a terminal and is multiplatform (Linux, Windows, MacOS, Android, iOS). It is called Geekbench.

To install it on Linux we first download it from its official page. We can do it from the page or from the terminal. We decompress it and run it.

<pre>
curl -LO http://cdn.geekbench.com/Geekbench-5.2.3-Linux.tar.gz
tar xf Geekbench-5.2.3-Linux.tar.gz
./Geekbench-5.2.3-Linux/geekbench5
</pre>

Once executed, it will start to perform the tests and at the end it will give us a URL to see the result.
