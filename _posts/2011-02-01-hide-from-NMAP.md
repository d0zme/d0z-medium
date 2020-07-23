---
title: Hiding Services from NMAP Using Non-Standard Ports
layout: post
tags: network
---

Most system administrators know that using non-standard ports for some services can be a useful way to hide ports from both automated attacks and less determined attackers. In addition, it is also a good way to lower the profile of an important host on your network, as an initial portscan of what is actually an important host might report nothing particularly attractive to an attacker if the services are using non-standard ports. But how should one go about choosing a non-standard port to use? Is one better than another?

As some may know, nmap, which is easily the most popular port scanning tool out there, will by default not scan all the ports on a system, as this is *very* slow and *very* noisy. Instead, nmap uses statistics gathered by the nmap developers to determine which ports will most likely be open on any given host, thereby greatly increasing the likelihood that a scan of 1000 ports will yield all the open ports on a system. While this is great for increasing scan speed and decreasing visibility, it brings with it a downside: that individuals wishing to hide ports can more easily hide from port scans if they wish to.

The statistics that nmap uses to determine common services are stored in an included "nmap-services" file. I have written a small script (available here) that parses this file and provides a list of ports in a provided range that are not included in the file. Any of these ports will, therefore, not be revealed to an attacker unless they already know the port number from some other research that they did on the host, or if they waste the time and take the risk of performing a full scan of all 65536 ports.

As an example, I started with a host that had port 80 (http) open and port 22 (ssh) open. This host, to an attacker performing a port scan of a network, could look rather tempting. Both ssh servers and http servers are interesting services, and could attract unwanted attention. In addition, these servers (especially ssh) are magnets for brute force attacks, filling up logs with tons of uninteresting garbage, making it hard to track the actually important information. Here is a screen shot of our example host:

![](https://i.imgur.com/06prx9N.png)

Using my tool, we can find other ports for these services to use that nmap won't easily find. I chose 242 for ssh and 8079 for http-alt, but it's arbitrary.

So many to chose from!

![](https://i.imgur.com/hGisjuX.png)

Ok, so now we just edit the configuration file for the respective services, restart them, and voila, we are invisible! Well, you know, almost.

![](https://i.imgur.com/3TT3r2j.png)

![](https://i.imgur.com/imvH2TH.png)

As you can see, an attacker will be forced to perform an exhaustive scan of the system to gain any useful information. Our two ports, 242 and 8079, only show up when we force nmap to scan every port on the system, which is definitely not fast or quiet, and many IDS systems will detect  this complete scan.

Now, obviously, this is not the solution to all your security problems. If you have an outward facing HTTP server, people need to know the port to access it, so no matter what port it's on an attacker  will be able to find it. However, if  your service has a very limited amount of people that need to know the port number, but that is also a very important service that will attract attacks (like ssh or http), then using a non-standard port could make sense, and using this method will make your important services basically invisible to all but the most determined attackers.

As always, any bugfixes or suggestions are definitely welcome. Enjoy!
