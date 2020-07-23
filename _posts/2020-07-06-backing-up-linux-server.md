---
title: Backup of Linux server and migration to a different server
layout: post
image: https://i.imgur.com/j21nAeD.png
---

I had worked in small company, and very often I do some stuff, related to system administration. Last week we were configuration FreePBX with Debian 7.8. While doing that we understood that server doesn't want to be loaded from HDD, when anything is connected to the USB. Further research didn't give any results. We decided to do the following:

- Backup the server
- Restore it on another server.
- Below you can find an easy way to do that.

## I had two options:

tar – zips all files and doesn't save MBR -> backup will weight about 1.5GB
dd – makes a full copy of the server -> with weight about 490GB.
For me it was easier to do tar, since the deploy and restore will be smaller. Also, in this case it's possible to write down the backup even on a flash driver.

## Here is the plan to do that:

- Create a backup
- Formatting and files system creation
- Backup restore
- MBR creation

## Testing
1. Backup creation
Loading from a live flash drive.

Switching to root:

> sudo su
Mounting the section, which will be archived

> mount -o ro /dev/sda1 /mnt
Mounting the flash drive to read/write:

> mount -o remount,rw /dev/sdb1 /lib/live/mount/medium
Everything is ready to create archives:

> tar -cvzpf /lib/live/mount/medium/backupYYYYMMDD.tgz --exclude=/mnt/var/spool/asterisk/monitor --exclude=/mnt/var/spool/asterisk/backup /mnt/
> Parameters: c — create, v — process information, z —gzip archiving, p — data about owners, f — writing to the file, -/mnt/ — catalog, which should be archived.

The process takes about 7-10 minutes.

## Unmounting

> umount /mnt
And rebooting

> reboot

## Restoring on a different hardware

## 2. Making file system
Loading from a live-drive and switching to the root:

> sudo su

Marking the disk with the help of cfdisk.

> cfdisk

Deleting all sections. I have created two new sections: one 490 Gb for / (sda1) and one 10 Gb for swap (sda2). For the system one shoulw have type 83 Linux, the second – 82 Linux swap / Solaris. Mark the system one as (bootable) and save the changes.

Creating the file system

> mkfs.ext4 /dev/sda1

##3. Unzipping

Mounting the sction

> mount /dev/sda1 /mnt

## Unzipping from the flash

> tar --same-owner -xvpf /lib/live/mount/medium/backupYYYYMMDD.tgz -C /mnt/ <pre> 
> Parameter --same-owner — saves owner and unzips, x — unzips from the archive, v — shows the info about the process, p — save access rights, f — indicates the file for unzipping, C — unzips in the category.

## 4. Creating MBR on a new disk

In order to create a boot record, mounting working catalogs to our root catalog. Mine, foe example, is /mnt. Catalogs /dev and /proc right now are used bu live-system, and we use bind parameter to get them available on both places: <pre> mount --bind /dev /mnt/dev mount --bind /proc /mnt/proc

Switching to a new system:

> chroot /mnt

Making swap for a new system:

> mkswap /dev/sda2

Mounting it

> swapon /dev/sda2

To make grub work, it's necessary to give the right UUID for sectors in fstab, since right there is data of a previous system.

> nano /etc/fstab

Opening second terminal under the root

> sudo su

Calling it

> blkid

Copying UUID to the current fstab.

Installing grub2:

> grub-install /dev/sda

There should be now problems if you install it on a clear disk. Updating the info from fstab

> update-grub

Getting back to Live system

> exit

Unmounting all catalogs

> umount /mnt/dev umount /mnt/proc umount /mnt

Loading from a hard drive

> reboot

### 5. Testing

>  ifconfig -a
