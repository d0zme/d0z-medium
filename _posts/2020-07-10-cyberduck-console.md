---
title: Cyberduck console operations with cloud storage
layout: post
image: https://i.imgur.com/yp31Vtx.png
---

Users are familiar with the graphic version of Cyberduck. And recently the console version was released. So, here we will talk about its possibilities in general and about its posibillities of operations with cloud storage.

## General information
Console version of Cyberduck is supported by all modern OS – MacOS, Windows, Linux. The program can be used as FTP and SFTP-client, for operations with different cloud services.

Documentation for console Cyberduck version is published on the official site. Unfortunately, the majority of important functions are not covered as wide as it could be. So, we will make it wider by ourselves.

## Installation

### MacOS

It is made by package manager Homebrew:

$ brew install duck

### Linux

Here is installation procedure for Ubuntu 14.04. Users of other distributions can find information in the official documentation.

In order to install console version of Cyberduck we need to add special repository:

  $ echo 'deb https://s3.amazonaws.com/repo.deb.cyberduck.io nightly main'>/etc/apt/sources.list
  $ echo 'deb https://s3.amazonaws.com/repo.deb.cyberduck.io stable main'>/etc/apt/sources.list


Then we add the clue:

  $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FE7097963FEFBE72



And launch the commands:

  $ sudo apt-get update
  $ sudo apt-get install duck


## Common operations with cloud storage

All commands for operating with cloud storage has the following form:

  $ duck -<argument> swift://<username>@auth.domainname.com/<object path> -p<password>


After accepting the command program will ask to write the name of user whose account is being used. You can switch off dialogue mode by the option –q.

Getting a file list in a container
You can get a file list by the option –l or --list:

  $ duck -l swift://username@auth.domain.com/<container path> -p <password>

> Listing directory images…
> 1.jpg
> 2.jpg
> 3.png

#### File download

Downloading file from the repository is made by

  $ duck -d swift://username@auth.https://linuxforums.org.uk/ <file path> <file name> -p <password>

## Opening file for editing on the local machine

With the help of console Cyberduck you can open files for editing on the local machine. After editing the new version of file will be loaded into the repository. Use option edit:


  $ duck --edit swift://<username>@auth.domain.com/<file path>  -p <password>


File will be opened by the application which is used for this format in this OS. Loading of the changed version will start automatically.

This function is convenient for those who place static websites in some special repository. For example, if you want to edit text quickly, you just need to launch this command.

Loading object into the repository

### General view of the command:

  $ duck --upload swift://username@auth.domain.com <full object path in the repository> <object path in the local machine> -p <password>


Draw your attention to the fact that you should give the full object path in the repository of this object. For example, if you want to save file myimage.png from container images, its path will be the following: /images/myimage.png.

Big (more than 2GB) objects are loaded partly.

### Objects versions and backups

Console Cyberduck version is a convenient tool for backing up and archiving of data. Let's look at these functions a bit deeper.

Imagine that we have directory on the local machine with data which should be regularly copied to the cloud storage. We wrote the script and added the Cron task which sends backup every day at the particular time.

Script:
  #!/bin/bash
  SWIFT_USERNAME=usernaem
  SWIFT PASSWORD=password to enter the repository
  SWIFT_AUTH_URL=auth.domainname.com
  BACKUP_PATH=backup path
  LOCAL_PATH=folder on the local machine path
  $ duck --upload swift://$SWIFT_USERNAME@$SWIFT_AUTHURL/$BACKUP_PATH/ $LOCAL_PATH --existing rename --password $SWIFT_PASSWORD -q

The clue --existing tells what to do with already existing files in the repository.

Option “rename" renames already existing backup adding time and date to the name.

You can do differential backup by the Cyberduck as well. The following option is for it:
  $ duck --upload swift://username@auth.selcdn.ru <full object path in the repository> < object path in the local machine > --existing compare -p <password>

After execution of this command the program will compare the loaded backup with already available by the size, date of change and checksum. If something differs, the 
previous version will be replaced by the current.

In case of using the operation “skip" only new (the ones that appeared in the local machine folder after the last upload) files. Already existing files won't be upload even if the was changed.

Finally, option “overwrite" just deletes the previous backup and uploads the new one without any comparing.

### Synchronization of the local files with repository files

File synchronization is a process which result is two directories (one is placed on the local machine, the other - in the repository) containing the same list of most 

recent files. If you edit, add, or delete some files on the local machine, the same thing will happen with files in the repository.

Synchronization is launched by the command

  $ duck --synchronize swift://<username@auth.domain.com>/<folder path in the repository> <folder path on the local machine>


Thanks to the synchronization function you are able to have the most recent backups. Here is the example of simple script:

  #bin/bash
  SWIFT_USERNAME=username
  SWIFT PASSWORD= password to enter the repository
  SWIFT_AUTH_URL=auth.domain.com
  BACKUP_PATH=backup path
  LOCAL_PATH=backing up folder path

and...

  duck --synchronize swift://$SWIFT_USERNAME@SWIFT_AUTHURL/$BACKUP_PATH $LOCAL_PATH --password $SWIFT_PASSWORD -q

It is enough to add the appropriate task into the cron, and data will be automatically synchronized with the specified period.

This will be useful for the owners of static web sites, too. In order to update the website they need to change files on the local machine and launch the synchronization.

## Copying files

In order to copy file from the one container to another use the following command:

  $ duck --сopy swift:// <username@auth.domain.com>/<full file path> <username@auth.selcdn.ru>/<new place of storing path>  -p <password>

#### Option -v

Option -v (or -verbose) is used to output information about all HTTP-request and responses, which are done while operations with repository, to the console. It helps to understand how third-party applications interact with the repository.

## Conclusion

Console version of Cyberduck is a handy tool for operations with cloud storage, which has wide possibilities.

The existing of such software may please Windows users as there were no console applications for operations with cloud storages based on OpenStack Swift and they had to use FTP-clients, which are not always convenient.
