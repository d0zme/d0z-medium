---
title: Comparison of File Systems For Your Linux, BSD, or Unix Server
layout: post
image: https://i.imgur.com/o62TeId.jpg
permalink: /comparison-of-file-systems-linux-bsd-unix
---

When it comes to file system performance & stability in servers, you will likely want to use a Unix-like operating system over Windows, especially with higher network loads. Of course, there are quite a few types to choose from, each with their own set of advantages.

Popular Unix/Unix-like Operating Systems for Servers include:
- Linux, like Red Hat, Debian, or Ubuntu 
- FreeBSD 
- IBM/AIX (certified UNIX) 
- HP-UX (certified UNIX) 
- Oracle Solaris 
- Illumos & Open Indiana (based on Solaris source code) 
- NetBSD 
- OpenBSD 

Once you choose your flavor of the operating system, you are tasked with formatting your drives with a file system to handle your precious data. While each operating system will have different sets of default file systems included their installers, you may even find yourself hacking a third-party FS into your server (like ZFS on Linux).

Let's go over the file systems that you may consider in the world of *NIX operating systems:

### Ext2

The Linux Second Extended File System 2 (Ext2) was introduced along with Linux with similarities to Berkley's FFS (or now known as UFS). It was used as the default file system in most Linux distributions until journaling files systems (Ext3 and Ext4) became popular. Modern usage of Ext2 may be in instances where journaling is not desired, like with volatile flash storage.

Every file and directory has its own individual inode (index node). Each inode contains information about the file, including permissions, which user owns it, and its location on the disk. This concept is carried out in Ext3 and Ext4.

 

Features of Ext2:
- A maximum file size of up to 2 Tebibytes (TiB) and volumes of up to 32 Tebibytes (TiB). 
- Shares many properties with traditional Unix file systems 
- Introduced the concept of index nodes 
- Can be mounted in most operating systems (with third-party software in Windows and MacOS) 

### Ext3

The Third Extended File System (Ext3) continues the work of Ext2 and introduces journaling, which improves reliability and reduces the need for file system checks. It was the primary standard in Linux distributions for most of the 2000s.

Ext3 does not compete well in current bleeding edge file systems, like Ext4 or ZFS, but it is the most logical upgrade point from legacy systems with Ext2. Ext3 may be directly upgraded from Ext2 without having to backup data, which is great for upgrading critical servers in a time-constrained setting.

Features of Ext3:
- Just like Ext2, Ext3 has a maximum file size of up to 2 Tebibytes and volumes of up to 32 Tebibytes. 
- Compatible utilities with Ext2 
- In-place upgrades from an Ext2 formatted disk. 
- The lower processing power required in comparison to some other journaling file systems. 
- One of the most widespread and tested file systems for Linux. 
- Htree directory indexing, which is also implemented into the Linux kernel. 

### Ext4

The Fourth Extended File System (Ext4) is what most modern Linux distributions use by default and is continuing development. It is yet another journaling file system and likely the most stable one available to Linux.

As expected, it is backward compatible with the features of Ext2 & Ext3, with mounting being native. If mounted in Ext4, the new features of the file system may also be applied.

One unique aspect of Ext4 is that it can pre-allocate space without having to zero-out the rest of the data. The data will remain contiguous without the risk of being overwritten by other data. It also uses a technique called allocate-on-flush to delay allocation until the data is flushed, which may save some system resources.

 

Features of Ext4:
- No limits on subdirectories 
- Supports larger block sizes 
- Dynamic inode allocation, which is not found in Ext3. 
- Max volume & file size of 16 Tebibytes 
- Persistent & delayed pre-allocation 
- Redundant superblocks, which aids with corrupt superblock recovery 
- Quotas moved from user space to the Linux kernel 

### UFS

The Unix File System (UFS) has a long legacy within Unix history and is arguably the most stable file system out there. It is used as one of the primary file systems for FreeBSD (aside from ZFS), Oracle Solaris, and is supported by most other Unix-like operating systems. UFS may be used without caching or journaling, making it suitable for volatile storage (like flash memory) as an alternative to Ext2.

Features of UFS:
- Very large maximum file size & volume size of 8 Zebibytes 
- Logging and snapshots for easy recovery 
- Issues state flags to show the state of the file system and reduce the need for time-wasting file-system checks. 
- Supported by modern 64-bit and 32-bit kernels 

### ZFS

ZFS is another default file system found in FreeBSD, Oracle Solaris, and Linux (with limited support). The design of the operating system is to diligently protect against data corruption and very efficient at compressing data or handling large volumes. It was created by Sun Microsystems (now Oracle) and is available for all Unix-like operating system thanks to the OpenZFS project.

While ZFS offers blazing fast speed and stability for a busy file server, it is quite demanding on systems with low amounts of ram. If you install FreeBSD or Solaris on a general purpose laptop or desktop, it is probably better to use UFS.

Features of ZFS:
- Max volume of 256 trillion Yobibytes (YiB) & max file size of 16 Exbibytes (EiB) 
- Doubles as a volume manager 
- Supports auto-snapshots and copy-on-write 
- Built-in RAID features 
- Per-block cryptographic checksumming 
ReiserFS/Reiser4

ReiserFS was the creation of Hans Reiser and was used for a period of time as the default file system by SUSE Linux Enterprise. Since the creator is now serving a life sentence in prison, volunteers maintain its code.

The file system one of the few journaled file systems designed for Linux and brought in some exciting features for its era. Most notably, online resizing allowed for shrinking or growing the file system without needing a volume manager. The file system has the best performance when dealing with a large number of tiny files (4 KiB), but it otherwise is outperformed by Ext4.


Features of ReiserFS:
- A maximum file size of 1 Exbibyte (EiB) and volume size of 16 Tebibytes (TiB) 
- Tail packing to prevent fragmentation 
- Metadata journaling 
- Online resizing 


### XFS


XFS is a 64-bit journaling file system that is usually an option within installers of most Linux distributions. This file system was actually created by Silicon Graphics to go along with their latest IRIX (UNIX) release, but it was taken up by the Linux community since the company is now defunct.

The file system is extremely efficient with file system bandwidth since it has parallel I/O. This is very useful for very large and demanding storage servers that need scaling performance. More features are planned with future developments in the Linux kernel, including snapshots and copy-on-writing.

One main drawback of using XFS is that resizing it requires manually backing up data and reinstalling it on a volume. Another is that there is no checksum protection when data is silently corrupted. You may only notice a performance increase against other mainline file systems when using multiple threads of file transfers.

Features of XFS:
- Maximum file size & volume size of 8 Exbibytes 
- Persistent pre-allocation 
- Parallel I/O 
- Metadata journaling 
- Write barrier supported 
- Continued development with the Linux kernel. 


### JFS/JFS2

The Journaled File System (JFS) is a journaling file system invented by IBM in the 1990s to be used with AIX and OS/2. It had also been adopted by Linux and other Unix/Unix-like operating systems. It was one of the first journaling file systems created and one of the first to be optimized for multiple processors.

JFS only journals a file's metadata, which means that the entirety of a file may still be corrupted. Compression is not supported in later versions of JFS2, and it had performance issues when it was implemented. Outside of AIX systems, JFS is rarely used in Linux or other operating systems.


Features of JFS:
- Max volume size of 32 Petabytes and max file size of 4 petabytes. 
- Still supported for latest changes in Linux 
- The B+ tree structure for faster lookups 
- Dynamic Inodes 
- Concurrent I/O to fight data inconsistency 
- SSD TRIM support 



### BTRFS

BTRFS (B-Tree File System) brings a set of features that are similar to ZFS, including per-block checksumming and volume management. In a realistic setting, BTRFS lacks performance in comparison to mainstream file systems and its stability as a volume manager is questionable. It has snapshot management as well, but it can be quite buggy.

Features of BTRFS:
- Volume management 
- Per-block checksumming 
- Max file size & volume size of 16 Exbibytes (EiB) 
- Copy-on-write file protection 
- Resource pooling 

## Conclusion

If you are unsure which file system you need and you are only installing onto a single-disk configuration, it is best to stick to the default file system that your operating system suggests. The cross between file systems as primary installation disks can cause instability as some file systems were developed for certain kernels (like Ext4 being Linux-specific). The type of hardware used should also influence your choice in file system, like non-journaling file systems being recommended for embedded systems with flash storage.
