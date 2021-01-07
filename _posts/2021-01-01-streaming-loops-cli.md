---
title: Streaming Video Loops to Twitch or Dlive from a command line terminal
layout: post
permalink: /streaming-video-loops-twitch-dlive
image: /images/twitch.png
---

Most people use OBS to stream from their desktop computers. However, if you are looking to stream looped videos to online streaming platforms from a unix-based server, it's not really a viable option.

Luckily, FFMPEG supports outputting video playback to RMTP servers.

Start out by installing FFMPEG on your system. For Debian/Ubunted based systems it's simply:
<pre>
apt-get install ffmpeg
</pre>

Packages are also available for *BSD, MacOS brew, and binaries for Windows.

While logged into your account, find out the ingest point for the RTMP protocol: http://stream.twitch.tv/ingests/

Copy your stream key under: https://dashboard.twitch.tv/u/YOUR_USERNAME/settings/channel

The video you want to use will work ideally with 720p resolution, but other SD resolutions should work fine without dropping frames.

With in the terminal, issue this command to start streaming:

<pre>
ffmpeg -stream_loop -1 -i VIDEO.mp4 -c:v libx264 -s 852x480 -r 30 -f flv "rtmp://YOUR_URL/STREAM_KEY?"
</pre>

With different platform ingest points, you can stream to Dlive, Instagram, Facebook and other obscure streaming platforms. If your home connection can handle it, you can mirror to multiple streaming website at once using multiple commands.
