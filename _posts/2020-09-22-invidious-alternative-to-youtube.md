---
title: Invidious an open source front-end alternative to YouTube to avoid snooping
layout: post
image: https://i.imgur.com/8fWgyi2.png
permalink: /invidious-alternative-to-youtube
---

**Update**: The Invidio.us website will soon be shutting down. We recommend using [Yewtu.be](https://yewtu.be) as an alternative, or creating your own instance using the instructions at the end of this article.

Invidious is an alternative front-end to YouTube that doesn't use the official YouTube API. Instead, it parses the YouTube site's source code to get the necessary information, similarly as projects like youtube-dl and NewPipe.

At the same time, it processes most user requests through the server where it is installed, which adds another layer of privacy for uers. The project code is written in the Crystal programming language, uses the DBMS PostgreSQL and is distributed under the AGPLv3+ license.

Invidious, in fact, is analogous to the quite popular previous web service HookTube, whose author, in July last year (a week after [Invidious](https://archive.is/9Kidy) was announced), received a warning letter from Google about its violation of the YouTube API terms of use and was forced to stop "normal" work on its service.

**HookTube's** main goal was to send users' requests to Google's servers (YouTube), which, while improving users' privacy, also allowed them to view and download videos (including those with geographic restrictions, for example).

Invidious is currently on a monthly release cycle and is intended to provide administrators of their own Invidious instances with more or less relevant and stable source code improvements.

## Invidious Features

Invidious allows users to view YouTube videos without advertising and without Google tracking. At this point, the Invidious API uses the FreeTube application, the MusicPiped music player and the CloudTube website.

On the other hand, it also highlights the possibility of importing / exporting subscriptions in Invidious (including the NewPipe format), the browsing history and the configuration. RSS support for YouTube and custom feeds.

As well as the ability to manage subscriptions, being able to show only unvisited videos and the latest videos, delivery of notifications about new videos, import of subscriptions from YouTube.

Another great feature of Invidious is the ability to embed videos with Invidious into the pages of other sites. Both directly and from YouTube (using a script).

It is also worth mentioning that Invidious provides its own API for developers. Of the other features that can be highlighted from this front-end we find

- Audio-only mode (no need to keep the window open on the mobile)
- Free software (AGPLv3 license)
- On Invidious there are no ads or user tracking
- No need to create a Google account to save subscriptions
- Light (home page is ~ 4 KB compressed)
- Dark mode
- Integrated support
- Set the player's default options (speed, quality, auto play, loop).
- The ability to view the video without the inclusion of JavaScript
- Support for Reddit comments instead of YT comments
- Does not use any of the official YouTube APIs
- Omission of blocks in case the video is not available for the user's country
- Developer API

For those who are interested in trying Invidious they should know that they can visit the web page where the service is installed.

Or they can download the front-end code and mount it personally on a server.

## How to install Invidious?

For those who are interested in mounting this front-end on a server or on their system in their personal computer. But first you need to have some dependencies that are necessary for the operation of Invidious, so we have to install them first.

If you are a user of Arch Linux, Manjaro , Antergos or any other derivative of Arch linux you must open a terminal and type the following:

<pre>
sudo pacman -S shards crystal imagemagick librsvg postgresql
</pre>

In the case of those who are users of Debian, Ubuntu or any derivative of these we are going to type the following:

<pre>
curl -sSL https://dist.crystal-lang.org/apt/setup.sh | sudo bash
curl -sL "https://keybase.io/crystal/pgp_keys.asc" | sudo apt-key add -
echo "deb https://dist.crystal-lang.org/apt crystal main" | sudo tee /etc/apt/sources.list.d/crystal.list
sudo apt-get update
sudo apt install crystal libssl-dev libxml2-dev libyaml-dev libgmp-dev libreadline-dev librsvg2-dev postgresql imagemagick libsqlite3-dev
</pre>

Having done this, let's now download the Invidious installer script:

<pre>
wget https://github.com/tmiland/Invidious-Updater/raw/master/invidious_update.sh
sudo chmod +x invidious_update.sh
sudo ./invidious_update.sh
</pre>
