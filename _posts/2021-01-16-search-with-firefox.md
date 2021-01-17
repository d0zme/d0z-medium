---
title: Changing the pinned Search With Google from Firefox in Linux or BSD
layout: post
image: https://i.imgur.com/iZ9idv4.png
permalink: /search-with-google-firefox
---

You probably already know that Firefox lets users search from the address bar with a "Search with Google" at pinned at the top. Even if you remove Google as a search option within **Preferences**, this pinned option will still show up, annoying fellow DuckDuckGo users. This is where you will have to dig a bit deeper.

*Note: This was tested on Linux and OpenBSD. It may be slightly different for MAC or Windows users.*

Within the o in the address bar type in **about:config** and press Enter or Return on the keyboard.

You will get the standard warning, just select **I’ll be careful, I promise!**.

Within the search bar, type in **browser.newtabpage.pinned** and edit this field by clicking on the **pencil icon**.

Switch the **google.com** URL to **DuckDuckGo.com**, **ecosia.org**, or whatever you preferred search engine happens to be. You should also switch the @google part of the string to something else.

Once you restart the browser, you should no longer encounter the annoying "Search with Google" pin.
