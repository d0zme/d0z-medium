---
title: What is Port 1?
layout: post
permalink: /port-1
---

### What it likely is: 1/tcp tcpmux TCP-Multiplexer 

It is as decribed in the original RFC

> TCP Port Service Multiplexer (TCPMUX)

> Status of this Memo
> 
>   This RFC proposes an Internet standard which can be used by future
>   TCP services instead of using 'well-known ports'.  Distribution of
>   this memo is unlimited.
>
> Overview
>
>   Ports are used in the TCP to name the ends of logical connections
>   which carry long term conversations.  For the purpose of providing
>   services to unknown callers, a service contact port is defined.  The
>   contact port is sometimes called the "well-known port".  Standard TCP
>   services are assigned unique well-known port numbers in the range of
>   0-255.  These ports are of limited number and are typically only
>   assigned to official Internet protocols.
>
>   This RFC defines a protocol to contact multiple services on a single
>   well-known TCP port using a service name instead of a well-known
>   number.  In addition, private protocols can make use of the service
>   without needing an official TCP port assignment.

> The Protocol

>  A TCP client connects to a foreign host on TCP port 1.  It sends the
>   service name followed by a carriage-return line-feed <CRLF>.  The
>   service name is never case sensitive.  The server replies with a
>   single character indicating positive ("+") or negative ("-")
>   acknowledgment, immediately followed by an optional message of
>   explanation, terminated with a <CRLF>.  If the reply was positive,
>   the selected protocol begins; otherwise the connection is closed.

> Service Names

>   The name "HELP" is reserved.  If received, the server will output a
>   multi-line message and then close the connection.  The reply to the
>   name "HELP" must be a list of the service names of the supported
>   services, one name per line.

>   The names listed in the "Protocol and Service Names" section of the
>   current edition of "Assigned Numbers" (RFC-1010 at this time) are
>   reserved to have exactly the definitions specified there.  Services
