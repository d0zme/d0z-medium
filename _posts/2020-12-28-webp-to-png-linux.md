---
title: Convert WebP images to PNG in Linux and BSD via the command line
layout: post
permalink: /webp-conversion-linux-bsd
image: https://upload.wikimedia.org/wikipedia/commons/thumb/0/06/WebPLogo.svg/800px-WebPLogo.svg.png
---

WebP is the updated web image format created by Google, primarily intended to leave a lighter footprint for websites. Impressively, they were able to create a new image format while [roviding a high compression ratio, leaving the original image quality in tact.

Having said that, it can be quite annoying to come accross a webp image and trying to upload directly to an image host that doesn't support it (like Imgur). Luckily, there are a couple command line programs that one could easily create bash script for bulk conversion.

## FFMPEG

You probably have ffmpeg installed on your Linux machine, and if not, it's available in just about any repository.


This simple command will produce a PNG image:

<pre>
ffmpeg -i image1.webp image2.png
</pre>

You may get a slew of error messages depending on your version, but it does indeed convert.

Here's an example of a bash script to help automate the process:

<pre>
#!/bin/bash
for a in ./*.webp; do
  old=$IFS
  IFS="\n"
  ffmpeg -i "$a" "${a[@]/%webp/png}"
  IFS=$old
done
</pre>


## Libwebp

While ffmpeg is great, it creates larger-than-desired images if you're looking to convert & store high quantities of images. This is where the native **libwebp** would be preferred.

For Debian-based distros, install via:

<pre>
# apt-get install webp
</pre>

For Arch-based distros:

<pre>
# pacman -S libwebp
</pre>

While this will make several new commands available, the command of interest is **dwebp**. Simply issue this line in a terminal window:

<pre>
dwebp image.webp -o image.png
</pre>

And to do the reverse process, use **cwebp**:

<pre>
cwebp -q 80 file.png -o file.webp
</pre>
