---
title: The easiest way to use PDAnet with Linux or BSD for unlimited tethering
layout: post
image: https://i.imgur.com/wLMcNre.jpg
permalink: /pdanet-on-linux-freebsd-unix
---
Mobile data is getting cheaper & faster, and you probably have an offer for unlimited 4G/5G in your local area. It usually comes with a catch of severely limited data allocations for tethering, and sometimes it isn't allowed at all.

[PDAnet](https://pdanet.co) is the easiest, and likely the most popular way to avoid tethering data caps. They have a nifty application for Windows & Mac OSX that allows you to tether with just a few clicks. For Linux, FreeBSD, or Chrome OS users, we are left to figure it out on our own.

Fortunately, if your *nix computer has a working Wifi adaptor, it's not so difficult to set up.

## Setting up PDAnet your phone

PDAnet is available through the Play Store, App Store, so you it's pretty straightforward to install. [APK binaries](http://pdanet.co/install/) are also available on their official website in case you have no other means of installing it.

Open up the app, and Click the checkbox for **"WiFi Direct Hotspot (new!)"** to create an access point.

You should then see blue highlighted text at the top. Take note of the **Name** and **Password** fields as they are always randomly generated so you will have to manually type them in each time.

**I have only tested this with Android, but it's possibly the same with the iOS, Windows Phone, or Blackberry versions of the app.**

## Setting up WiFi on your Linux/BSD box

Using your WiFi network-manager, search for your randomly generated access point and connect to it using the password generated in the app.

You will then be connected as normal, but you are still not ready to browse the web as with normal WiFi Tethering. An HTTP proxy will be hosted at **http://192.168.49.1:8000** and you will only have access to the internet through it.

## Browsing the web

If you only need to use your web browser, simply set your proxy settings to **192.168.49.1:8000**.

**In Firefox**, go to **Preferences -> Network Proxy -> Settings**, and fill out your **Manual Proxy** settings to:

<pre>
  HTTP Proxy: 192.168.49.1 

  Port: 8000
</pre>

**For Chromium or Chrome**, you will set the proxy via the command line:

<pre>
chromium-browser --proxy-server="192.168.49.1:8000"
</pre>

And be sure to check **Use this proxy server for all protocols**

## Using Apt-get (Apt) with PDAnet

On a Debian-based distro, you can install updates with APT by setting up your proxy settings.

<pre>
  sudo nano /etc/apt/apt.conf.d/proxy.conf
</pre>

Add this line to your **/etc/apt/apt.conf.d/proxy.conf** file:

<pre>
  Acquire::http::Proxy "192.168.49.1:8000";
</pre>

Save the **proxy.conf** file. 

## Proxychains with PDAnet

You may force a program to use your PDA proxy with proxychains.

Add your servers to the end of **proxychains.conf**, removing any other servers that happen to be in the file:

<pre>
  [ProxyList]
  https 192.168.49.1 8000
</pre>

## Wrapping up

**PDAnet** is a a nifty tool for travelers like me, but the trial version has the the annoying part of disconnecting you every 15 minutes. Unless you only need brief, sporadic tethering sessions, it's entirely worth the $15 license.

Also, **please don't abuse your connection** with torrents, as you never know what other traffic shaping methods your carrier will hail down upon you.

---

Article translated in: [ES](https://d0z.me/es/pdanet-linux-freebsd-unix)
