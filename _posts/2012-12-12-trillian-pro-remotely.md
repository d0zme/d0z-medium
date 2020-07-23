---
title: Accessing Trillian Pro Remotely and Through an Encrypted Tunnel
layout: post
tags: network
---

I am writing this because I constantly run into situations where people want to do things like browse the web, or talk over the net but they don't want their office to see what they are doing over the network. Also a lot of security content filters block certain ports from being used. Some vendors claim that they block "all chat services". Basically there is one of two ways in which they do this.

The two methods are: by port or by protocol. By port means they look for common chat ports (like port 5222 for AIM) and block them. By protocol means they look for what a chat session headers look like and block them (this is typically harder to get around, and what most vendors claim is really good security). I'm going to show you a way to bypass both of these methods. To do this you will build a secure (encrypted) tunnel to a remote machine through the blocking or monitoring device and use your remote machine as a proxy server.

Most of the time changing your AIM and Yahoo ports to port 25 (SMTP - send mail transfer protocol) will bypass any firewall rules that stop you from chatting but once in a while I run into a situation where using an encrypted tunnel is the only way to go. Using this document there will be no way for your office to sniff your traffic on the wire. Although it should be noted that your office always has access to your computer if you step on their premesis or authenticate to their primary domain controller, so just be wary. Also, it is typically against most companies' acceptable use policy to bypass their security, so chances are they would frown on this. So consider this document as educational only.

You will need two machines for this set-up to work. One machine on a static connection (we'll call this the server) that you can connect to on port 22 (or some other port that you designate as the SSH [secure shell] port) and the machine you will be working from (client). SSH is the encryption part of this technique. This has nothing to do with the encryption built into Trillian Pro, but works in a vaguely similar way. I will explain it all in terms of Windows. But you could do this with Trillian Pro inside a VMware session or something else if you are a devout Windows hater.

By "static connection" I mean somewhere that has an IP address that you can connect to that doesn't change, but you can also use a service like http://www.dyndns.org/ to make a dynamic connection appear static. If you cannot do port forwarding or cannot host a machine on your broad-band connection, stop now, and find a friend who will let you host a machine at their house. So without further interruption, here is the definitive guide for using Trillian Pro remotely (works with AIM, IRC, ICQ, Yahoo and MSN) as well as how to build an encrypted HTTP (hyper text transfer protocol) tunnel all in one document.



# Step 1: Install the correct software on the server:

On the server:

Install Cygwin from http://www.cygwin.com. Cygwin is a UNIX emulator for Windows. Really we are only using it for the sshd and apache services, so if you know of another way to get those working that you like better, feel free to use those. Please note that I am assuming in this document that you are installing it in C:/cygwin/

- Make sure you install at the least these services:
- apache (web-server) - this will be your proxy server
- pico or vim (editor) - this is optional, but recommended
- cygrunsrv (to install services)
- openssh (your ssh server) - this is the server half of the encrypted tunnel.
- shutdown 

-Install Trillian Pro (sorry, the freebee version won't work with the plugin) from http://www.trillian.cc
-Install I.M. Anywhere Plugin from http://www.iknow.ca/imeverywhere/ 



# Step 2: Configure the server:

On the server:

- Get SSHD working:
- Load up Cygwin and type "ssh-host-config -y" You have now configured SSHD (secure shell daemon)
- Now type "cygrunsrv -S sshd" and this will start the daemon (you will need to do this every time you reboot or you will need to add it to your startup files.)
- Load up cygwin and edit the following file /etc/apache/httpd.conf with vim or pico OR browse to your cygwin directory and edit it via another (non-cygwin) editor. The file (httpd.conf) will probably be located in C:/cygwin/etc/apache/.

Put the following lines in the apache conf file (put them at the end for ease of finding them again). Note: the 127.0.0.1 is called "loopback", which is a reserved IP. That line essentially limits the proxy from being accessed by anyone who is not located at the computer or who is not SSHing into it. Don't change that line unless you know what you're doing.

        	ProxyRequests On
        	ProxyVia On

        	<Directory proxy:*>
        	Order deny,allow
        	Deny from all
        	Allow from 127.0.0.1 
        	</Directory>
        	

Now let's start apache. In cygwin type "/usr/sbin/apachectl start" (Don't shut down cygwin after you are done doing this).

Now, let's load up Trillian Pro and make sure the I.M. Everywhere module is turned on.

Create a username and password and put the port on 8000 (or some other port other than 80 since that is where your proxy server is going to live). Actually you could combine these two processes into the one proxy server, but for complexity's sake, let's just make them two. If you want to combine them read this. 



# Step 3: Download software for the client:

On the client:

Install Internet Explorer if you don't have it already (yes, other browsers will work, but I won't be going into those).

Download PuTTy (putty.exe) from http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html (PuTTy is the client half of the encrypted tunnel). 

You can also use Stunnel here instead of PuTTy and SSHD, but I don't like it as much, primarily because it is not one single, self contained binary and it has all sorts of weird interoperability issues with itself. IE: you will need to download the OpenSSL libraries seperately for the correct version if you use Stunnel. Also, the PuTTy binary is around 200k in size, where the Stunnel binary bundle is around 1.4 megs (so around 7 times the size). I will probably add a Stunnel version to this document later, since it involves less components, and therefore theoretically an easier install (take a look at this for ideas if you are impatient). 



# Step 4: Configure the client:

On the client:

Now configure configure PuTTy. Load it up and type in the remote IP address (or host name if you have one) of the server in the "Host Name (or IP address)" field. Select port 22 (unless you changed it). 

Now go to the "Tunnels" tab on the left under Connection->SSH->Tunnels. Select the source port as port 80 and the Destination as the IP address of the server (not the client!) and the port you want to connect to (so something like 123.123.123.123:80). And click the "Local" option button and click "Add". Now go back to the "Session" tab on the left and name it something in the "Saved Sessions" tab. Something like "HTTP Forward" will do. Click "Save" and then click "Load". You should be prompted with a user name for your remote server. Type in your server username and password and you should be connected.

Now go to Internet Explorer. Under Tools->Internet Options->Connections->Lan Settings you will find "Proxy Server" Select the option to use a proxy server and in the address filed type "localhost" and port "80". 



# Step 5: Using Trillian Pro Remotely:

On the client:

In Internet Explorer go to http://localhost:8000 (note if you changed the port to be something other than 8000 use that port here). Log in with the I.M. Everywhere password you selected on the server. Wait for the pop-up, or if you use Google's toolbar, click the link and Trillian Pro should load up in your Internet Explorer Window. (You do not have to keep the browser location set at http://localhost:8000 after the window pops up.) 



# Step 6: You're Done!
You can now surf the web or access Trillian Pro remotely and securely through content filters and firewalls.

Some Last notes:

- Make sure you keep the SSH daemon and Apache daemon running on your server when you leave so that you will be able to connect.

- Make sure you keep open the Trillian Pro window on your client and the PuTTy window connected to the server, or this will break.

If your home network (or wherever your server lives) has port 22 for your ssh server blocked, try other ports (below 65535). Often you will find one that your providers won't block. Look at the ports list for ideas. Often you can put it on port 80, since it is unlikely that your office will block port 80 ingress/egress, assuming your server network doesn't block port 80 ingress/egress. This can be tricky if you are dealing with two networks that have content filters on both sides, but almost always you can figure something out on a high port unless it is a highly restrictive security policy.

For security reasons you should put your server behind a firewall that has port forwarding capability and configure it to only forward port 22 ingress (or whatever port you are using to forward to your host). You don't need the webserver port open since you are SSHing to the server and accessing it through the localhost. 
