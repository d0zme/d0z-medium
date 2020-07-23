---
title: Common VPN Error Messages
layout: post
---

# VPN Error 691

"Access denied because username and/or password is invalid on the domain" - On user may have entered the wrong name or password when attempting to authenticate to a Windows VPN. For computers part of a Windows domain, the logon domain must also be correctly specified.
Also be sure that you have selected the server destination correctly.

# VPN Error 806

"A connection between your computer and the VPN server has been established but the VPN connection cannot be completed." - This error indicates a router firewall is preventing some VPN protocol traffic between client and server. Most commonly, it is TCP port 1723 that is at issue and must be opened by the appropriate network administrator.

# VPN Errors 812, 732 and 734

"The connection was prevented because of a policy configured on your RAS/VPN server" - On Windows VPNs, the user attempting to authenticate a connection may have insufficient access rights. A network administrator must resolve this problem by updating the user's permissions. In some cases, the administrator may need to update MS-CHAP (authentication protocol) support on the VPN server. Any of these three error codes may apply depending on the network infrastructure involved.


# VPN Error 720

"No PPP control protocols configured" - On a Windows VPN, this error occurs when the client lacks sufficient protocol support to communicate with the server. Rectifying this problem requires identifying which VPN protocols the server can support and installing a matching one on the client via Windows Control Panel.
Also be sure that you have selected the server destination correctly.

# VPN Error 721

"The remote computer did not respond" - A Microsoft VPN reports this error when failing to establish a connection, similar to the error 412 reported by Cisco clients.

# VPN Error 412

"The remote peer is no longer responding" - A Cisco VPN client reports this error when an active VPN connection drops due to network failure, or when a firewall is interfering with access to required ports.

# VPN Error 51

"Unable to communicate with the VPN subsystem" - A Cisco VPN client reports this error when the local service is not running or the client is not connected to a network. Restarting the VPN service and/or troubleshooting the local network connection often fixes this problem.

# VPN Error 619

"A connection to the remote computer could not be established" - A firewall or port configuration issue is preventing the VPN client from making a working connection even though the server can be reached.

# VPN Error 800

"Unable to establish connection" – The VPN client cannot reach the server. This can happen if the VPN server is not properly connected to the network, the network is temporarily down, or if the server or network is overloaded with traffic. The error also occurs if the VPN client has incorrect configuration settings. Finally, the local router may be incompatible with the type of VPN being used and require a router firmware update.
