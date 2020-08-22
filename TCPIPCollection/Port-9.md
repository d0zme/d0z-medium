---
title: What is port 5?
layout: post
permalink: /port-9
---

If you encouter port 9 being utilized on your network, it's likely to be:
- **Discard (tcp,udp,sctp)**

## About Discard

Not to be confused with Discord, Discard is a test port that discards any input.

It is defined in the [RFC 4960](https://tools.ietf.org/html/rfc4960):

<pre>
Status of This Memo

   This document specifies an Internet standards track protocol for the
   Internet community, and requests discussion and suggestions for
   improvements.  Please refer to the current edition of the "Internet
   Official Protocol Standards" (STD 1) for the standardization state
   and status of this protocol.  Distribution of this memo is unlimited.

Abstract

   This document obsoletes RFC 2960 and RFC 3309.  It describes the
   Stream Control Transmission Protocol (SCTP).  SCTP is designed to
   transport Public Switched Telephone Network (PSTN) signaling messages
   over IP networks, but is capable of broader applications.

   SCTP is a reliable transport protocol operating on top of a
   connectionless packet network such as IP.  It offers the following
   services to its users:

   --  acknowledged error-free non-duplicated transfer of user data,

   --  data fragmentation to conform to discovered path MTU size,

   --  sequenced delivery of user messages within multiple streams, with
       an option for order-of-arrival delivery of individual user
       messages,

   --  optional bundling of multiple user messages into a single SCTP
       packet, and

   --  network-level fault tolerance through supporting of multi-homing
       at either or both ends of an association.

   The design of SCTP includes appropriate congestion avoidance behavior
   and resistance to flooding and masquerade attacks.
</pre>
