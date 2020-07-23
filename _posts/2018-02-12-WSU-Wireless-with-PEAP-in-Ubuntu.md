---
title: WSU Wireless with PEAP in Ubuntu
layout: post
tags: linux
---

This guide shows how to use the new WSU PEAP wireless deployment with Ubuntu 7.10+ and should work with the various derivatives such as Kubuntu.

This guide assumes you are using Network Manager which is installed by default. If you have chosen to use a different window manager than is default you may need to take steps to launch Network manager

- Download WSU's intermediate certificate to /etc/ssl/certs/
- Left click on the Network Manager icon on your menu bar.
- Select "WSU Wireless" from the list of choices. If more than one is available, select the one with the strongest signal.
- This will bring up a screen that looks like:
- Change "Authentication" to Protected EAP (PEAP).
- Click on the "CA Certificate" button which will open up a file dialog:
- Click on "File System" (on the left) and navigate to "/etc/ssl/certs/", select the file "wsu.pem", and then click the "Open" button.
- In the "User Name" field enter your WSU Network ID, and in the "Password" field enter your WSU Network ID password (this is the same username/password that you use for my.wsu.edu).
- Click "Connect" and start surfing the web.

And thats it! Now each time your computer detects the "WSU Wireless" network and no ethernet connection it will connect with these settings automatically. No more having to connect to the network and then activate the VPN or anything.

### Note

Try saving and using this file : http://www.wsu.edu/wirelessinfo/certupdate/cert/ssl123_pkcs7.p7b

If your OS doesn't like .p7b for whatever reason you can convert it by commanding:

$ openssl pkcs7 -print_certs -in ssl123_pkcs7.p7b -out wsuwireless.cer
-- and then trying to use the "wsuwireless.cer" that you just created.

or

$ openssl pkcs7 -print_certs -in ssl123_pkcs7.p7b -out wsuwireless.pem
-- and then trying to use the "wsuwireless.pem" that you just created.
