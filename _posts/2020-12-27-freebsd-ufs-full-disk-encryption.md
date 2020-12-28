---
title: FreeBSD Full-Disk Encryption on a UFS Root Partition
layout: post
permalink: /full-disk-encryption-ufs-freebsd
image: https://en.wikipedia.org/wiki/File:VirtualBox_FreeBSD_12.1_07_05_2020_11_59_43.png
---

The FreeBSD community is quite adamant of the operating sytem's ability to setup ZFS with ease & stability. So much so that it's the default file sytem when using a guided full-disk encryption installation.

For an antiquated laptop with limited resources, I don't really need the ZFS bloat, but I do understand it's advantages. That's why I created this concise guide for like-minded BSD users that prefer to revert to UFS while still maintaining a stable full-disk encryption.

## Setting up partitions

Once you've booted into the FreeBSD installer, drop into a Shell instead of doing the typical Install route:

![FreeBSD Installer](https://i.imgur.com/ETLO6Ui.png)

Now that you are at the command line, you will need to figure out which block device is associated with your hard drive. You may do this using:

<pre>
gpart show
</pre>

Since **ada0** is a typical example, we will go with this for now. Just to make sure, it's a good idea to destroy the current partition table and write a brand-new GPT table:

<pre>
gpart destroy -F ada0
gpart create -s gpt ada0
</pre>

If using a legacy BIOS, you can simply create a dedicated boot partition:

<pre>
gpart add -t freebsd-ufs -l freebsd-boot -a 4k -s 200m ada0
newfs -t -U -L bootfs /dev/gpt/freebsd-boot
</pre>

For thos using a **UEFI**-only system, be sure to **prior to the above step** using this chain of commands:

<pre>
gpart add -t efi -l freebsd-efi -a 4k -s 800k ada0
newfs_msdos /dev/gpt/freebsd-efi
mount -t msdosfs /dev/gpt/freebsd-efi /mnt
mkdir -p /mnt/EFI/BOOT
cp /boot/boot1.efi /mnt/EFI/BOOT/BOOTX64.efi
echo BOOTx64.efi > /mnt/EFI/BOOT/STARTUP.NSH
umount /mnt
</pre>

When you have all that resolved, you are free to create the root partition for your hard drive (where your main files will be stored):

<pre>
gpart add -t freebsd-ufs -l freebsd-root -a 4k ada0
</pre>

## GELI Encryption Setup

You should remain in the command line after creating your root partition.

Wrapping your root partition in an encrypted GELI container is as simple as running this command:

<pre>
geli init -b -e AES-XTS -l 256 -s 4096 /dev/gpt/freebsd-root
</pre>

You will then be asked to create a passphrase. Be sure to create something quite long, complex, yet easy enough to remember for daily use. With a decent password, it would be unlikely anyone will be able to steal your files if you laptop is ever stolen.

Then let's attach the partition so it's usable by the installer:

<pre>
geli attach /dev/gpt/freebsd-root
</pre>

Now you may go ahead and format this container partition into the UFS file system:

<pre>
newfs -t -U -L rootfs /dev/gpt/freebsd-root.eli
</pre>

Now set a mount point to be used within the installer:

<pre>
mount /dev/gpt/freebsd-root.eli /mnt
</pre>

As a duct-tape hack, we also need to create a symbolic link to the boot loader's directory:

<pre>
mkdir /mnt/bootfs
mount /dev/gpt/freebsd-boot /mnt/bootfs
cd /mnt
mkdir bootfs/boot
ln -s bootfs/boot
</pre>

To make the file system bootable, edit the fstab and loader.conf as so:

<pre>
vi /tmp/bsdinstall_etc/fstab
</pre>

and add the lines:

<pre>
/dev/gpt/freebsd-root.eli /       ufs rw 1 1
/dev/gpt/freebsd-boot     /bootfs ufs rw 0 0
</pre>

<pre>
vi /tmp/bsdinstall_boot/loader.conf
</pre>

and add the lines:

<pre>
geom_eli_load="YES"
vfs.root.mountfrom="ufs:ada0p3.eli"
</pre>

Now you are free to issue the **exit** command within the shell to return to the original menu. This time, select the Install option and continue as if it were a regular installation.
