---
title: Fish Shell, a smart alternative to Bash for GNU/Linux
layout: post
image: https://i.imgur.com/7ZTtKwe.jpg
permalink: /fish-shell-linux
---

Fish is a smart and user friendly Shell. Arrived at version 3.1.2, released last April, it has many interesting features. Distributed as open source software, it is available for GNU/Linux, BSD, MacOS and Windows.

## Fish or friendly interactive shell

A shell is a program that allows you to interact with the operating system by starting, for example, other programs. Fish offers a command-line interface focused on usability and interactive use. The main features of this shell are the syntax that can be highlighted, tab completion and automatic suggestions ready to use, with no configuration required.

![](https://i.imgur.com/f7zIZ2b.png)

When a command is executed in the shell, it is inserted at the end of the history file located in ~/.local/share/fish_history. You can save a command in the history without running it using the combination Alt+#. An interesting feature for Fish history is the ability to filter the history. By entering some characters and then pressing the up arrow key, a search is performed in the history of commands that include typed characters.

![](https://i.imgur.com/fo3SQf7.png)

## Incognito mode, Vi mode and web config

Very useful also the incognito mode. Fish does not insert any command that starts with a space in its history file. This can also be done with the -private flag, which prevents all subsequent commands from being recorded in the history file. Added also the variable $fish_private_mode to detect if a script is running in private mode.

![](https://i.imgur.com/mLdkIVL.png)

The default key associations used by Fish to move the cursor on the command line come from the Emacs editor. Examples are Ctrl + A to move the cursor to the beginning of a command, Ctrl + E to move to the end of a command, and so on. Fish 2.2 has introduced Vi mode for those who prefer shortcuts from the Vi editor.

![](https://i.imgur.com/opSZP6p.png)

## Web playground and installation guide

A web configuration tool is also available. It can be started with fish_config, and allows you to customize the prompt style, color theme and so on. Do you want to try Fish before installing it on your system, so you can see if you like it? You can do it through this site where there is a web playground made just for this purpose.

Installing Fish on GNU/Linux is very simple, depending on your distribution you just need to follow one of the following guidelines:

#### Ubuntu

<pre>
sudo apt-add-repository ppa:fish-shell/release-3
sudo apt-get update
sudo apt-get install fish
</pre>

#### Fedora

<pre>
dnf install fish 
</pre>

#### Arch

<pre>
pacman -S fish 
</pre>

#### Gentoo

<pre>
fish emerges 
</pre>

#### FreeBSD

<pre>
pkg install fish
</pre>

For all the details about Fish, which includes many advanced features, I refer you to the official project documentation, which you can access through [this link](https://fishshell.com/docs/current/index.html).
