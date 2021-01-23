---
title: How to Loop Mount an Raspberry Pi Image Before Flashing to SD Card
layout: post
permalink: /raspberry-pi-loop-mount-image
image: https://i.imgur.com/P9jFgro.jpg
---

If you download Raspbian, FreeBSD, or any other disk image for the Raspberry PI, chances are you will want to make a few changes before burning it to your SD card. Loop mounting is the best way to do this, and it doesn't have to be over-complicated.

The first step will be to install **kpartx**, which is available on any Debian-based linux distribution:

<pre>
apt install kpartx
</pre>

## Create a Loop Mount

<pre>
sudo kpartx -v a image.img
</pre>

## Create a Directory for the loop

<pre>
mkdir -p PI
sudo mount /dev/mapper/loop0p1 PI
cd PI
</pre>

Change **loop0p1** for **loop0p2** to access the ext4 file system. The partition  **loop0p1** will contain **config.txt** and the kernel images.

Go ahead and edit the contents as you wish.

## Unmount the loop

<pre>
cd ..
sudo umount PI
kpartx -v -d image.img
</pre>

## Burning your new image 

<pre>
dd if=image.img of=/dev/mmcblk0p1 status=progress
</pre>
