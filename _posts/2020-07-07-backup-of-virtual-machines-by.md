---
title: Backup of virtual machines by hypervisor QEMU/KVM
layout: post
permalink: /Backup-of-virtual-machines-by-hypervisor-QEMU/KVM
image: https://i.imgur.com/mpwrk2d.png
---

A lot of people know that backups are vital. Moreover, you need to do them in such way that you can recover them further. Especially, it is important in case of virtual machines (VM). So, let's take a look on backup facilities of the hypervisor QEMU/KVM for virtual machines' disks.

We can distinguish two main problems in this process. The first is the need to get consistent backup. It means that if, for example, we have a DBMS or another software, which uses its own cash for recording, we should ask it to reset cash and stop recording on the disk before the backup in order to get snapshot of the necessary for recovering data. The second is productivity of VM in a snapshot mode as we want it not to slow down while taking a copy and while deleting of snapshot.

Solution of the first problem: in order to get consistent backup you should shut down VM by guest OS.

If you want to back up without shutting down your VM, you should use QEMU guest agent (fo not confuse it with QEMU SPICE guest agent and with paravirtualized drivers for QEMU itself). In Debian Jessie repository it is qemu-guest-agent package, in Wheezy package is available only through wheezy-backports. QEMU guest agent is a small utility which accepts commands from host by vireo-channel named org.qemu.guest_agent.0 and executes them as a guest. On the hypervisor's side channel ends with unix-socket where you can write text commands by socat utility. By the way, Libvirt likes to use this channel, so if you use Libvirt to manage hypervisor, you will have to communicate with our guest by “virsh qemu-agent-command". QEMU guest agent can do different commands. Here it is list of our commands:

•	guest-set-vcpus

•	guest-get-vcpus

•	guest-network-get-interfaces

•	guest-suspend-hybrid

•	guest-suspend-ram

•	guest-suspend-disk

•	guest-fstrim

•	guest-fsfreeze-thaw

•	guest-fsfreeze-freeze

•	guest-fsfreeze-status

•	guest-file-flush

•	guest-file-seek

•	guest-file-write

•	guest-file-read

•	guest-file-close

•	guest-file-open

•	guest-shutdown

•	guest-info

•	guest-set-time

•	guest-get-time

•	guest-ping

•	guest-sync

•	guest-sync-delimited

Short description of every command you can find in qga/qapi-schema.josn file in QEMU sources. And full description can be found by analyzing qga/commands-posix.c and qga/commands-win32.c files. After it you will find out that commands guest-set-vcpus, guest-get-vcpus, guest-network-get-interfaces, guest-suspend-hybrid, guest-suspend-ram, guest-suspend-disk are not supported by Windows and guest-fsfreeze-freeze/guest-fsfreeze-thaw commands attempt to use volume shadow copy service (VSS). Nevertheless, we are talking about Linux as a guest OS, so we do not need these nuances.

Well, we are interested in following commands: guest-fsfreeze-freeze and guest-fsfreeze-thaw. First of them “freezes" guest file system, second – “unfreezes" it. Command (to be honest, it's IOCTL) fsfreeze is not a QEMU feature but it is a capability of guest's virtual file system. So that, you are able to freeze file system not only in virtual environment but on real hardware, too. It is enough to use fsfreeze utility from util-linux package. Its manual says that Ext3/4, ReiserFS, JFS, XFS are supported, but during the experiment it freeze Btrfs as well. Between processing flow of records and freezing itself kernel calls sync() (file fs/super.c, line 1329), so data integrity is secure. At all, kernel needs freeze FS in order to get complete snapshot of VLM-volumes.

So far we know that we call guest-fsfreeze-freeze function by QEMU guest agent to take complete snapshot. However, if we use Libvirt, we can give virsh shell parameter –quiesce, which will call guest-fsfreeze-freeze while creating the snapshot:

virsh snapshot-create-as myvm snapshot1 "snapshot1 description" --disk-only --atomic –quiesce.

But if we use Proxmox (pvetest branch) or Openstack, we can't do something similar. That's why you have to change the source code to automate calling guest-fsfreeze-freeze function.

For example, we have found a way to freeze guest FS before taking the snapshot. Now we should alert guest software before freezing itself. QEMU guest agent supports parameter –F, which says us that before freezing and after unfreezing we should call /etc/qemu/fsfreeze-hook script. That is the reason why we should add DAEMON_ARGS="-F" into start-agent script (/etc/init.d/qemu-guest-agent). Take into account that if script ends with error, freezing of FS will not run.

For MySQL server you can easily write this script:

#!/bin/bash 
USER="<Пользователь>" 
PASSWORD="<Пароль>" 
case "$1" in 
freeze ) 
/usr/bin/mysql -u $USER -p$PASSWORD -e "FLUSH TABLES WITH READ LOCK;" 
exit $? 
;; 
thaw ) 
/usr/bin/mysql -u $USER -p$PASSWORD -e "UNLOCK TABLES;" 
exit $? 
;; 
* ) 
logger Fsfreeze script has activated with unknown parameter: $1 
exit 1 
;; 
esac 
exit 1
But it wouldn't work as locking from the base will be removed after this command:

mysql -u $USER -p$PASSWORD -e "FLUSH TABLES WITH READ LOCK"
because all MySQL blocks work only when user made them is in system. If you want to do the proper backup, you have to write some additional service (in Python, for example), which would open MySQL base , make locking after freeze command, and then keep the base open and wait for the command thaw.

And what if we have Windows as a guest OS? We should mention that for Windows and MS SQL QUEM guest agent automatically calls an appropriate VSS-function, and VSS informs all subscribes that backup will start soon.

So, we blocked MySQL sheets and freeze guest FS. Now it's time to back up. Suppose that we store the VM disk images in qcow2 format, not as LVM-volumes, for example. Even in this case we have great amount of possibilities. Let's take a look over them.

![](https://web.archive.org/web/20160310033322im_/https://bitcalm.com/media/2015/4/4/Screen%20Shot%202015-04-04%20at%2011.32.18.png)

Each variant has its own pros and cons. In this way, Internal method is standard for Virt-Manager utility and for Proxmox environment, and taking of snapshots is automated here. But in order to get snapshot out of the file NBD-server on qemu-nbd base should be raised, and image file should be connected to it. In case of using External method prepared for copying backup file is obtained during taking the snapshot. Unfortunately, deleting of snapshot isn't an easy process as it calls for block-committing of recorded data from snapshot file to the basic image. It is accompanied by fold increase in the load on the recording while deleting the snapshot. For example, VMWare ESXi performance falls in 5 times in this situation. One more method to delete External-snapshots should be mentioned: copying all blocks from the source image to the snapshot. This method is called “block-stream".

LVM-volume snapshot causes a drop in the performance of the main volume on record, so it is best to use when we are confident that during the existence of the snapshot nothing will be writing intensive to the disk.

BTRFS as file system for disk images repository opens up great prospects because in this case snapshots, compression and de-duplication are provided by the FS architecture. Cons – BTRFS cannot be used as a shared file system in a clustered environment. In addition, Btrfs is a relatively new FS and perhaps it is less reliable than a bunch of LVM and ext4.

The method of obtaining backups by the command drive_bakcups is convenient because you can immediately create a backup on the mounted remote repository, but it puts a heavy load on the network. For the rest of the methods transmission only of the rsync changed blocks can be envisaged. Unfortunately, QEMU backup does not support transmission only of the “dirty" (changed after the last backup) blocks. In VMWare CBT mechanism it was realized. Both attempts to realize it in QEMU (livebackup and in-memory dirty bitmap) were not added to the main QEMU branch. Why? The first, probably, because of its architecture (one more daemon and single network protocol are added only for this operation). The second because of its obvious restrictions on the use: map of the “dirty" blocks can only be stored in the RAM.

In conclusion, let us consider a situation in which the VM has several connected disk images. Obviously, you have to do snapshots of all disks at one moment. In Libvirt snapshot synchronization is done by the program itself. But if you want to run this operation by the “clean" QEMU, you will choose between two possibilities: to stop VM by command “stop", get snapshots, and continue execution of VM by command “cont" or use the mechanism of transaction execution of commands available in QEMU. Only QEMU guest agent with guest-fsfreeze-freeze/guest-fsfreeze-thaw command cannot be used as though the agent "freezes" all mounted file system by one command, it is done not simultaneously but sequentially, so that desynchronization between volumes can appear.
