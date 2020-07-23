---
title: Google and the mystery of the 1e100.net domain that controls the internet
layout: post
---

Since last October you can see threads in forums asking why Google generated commands from the domain 1e100.net, instead of google.com. It was thought then that it was one more geekada of Google, very given to these things geeks, since 10 raised to 100 is a googol (a googol).

However today, the English newspaper The Register has published an article on the mysterious domain 1e100.net that "is being visited by about 3% of all Internet users, making it the 44 most visited domain according to Alexa in just three months:

After asking Google what's going on with this domain, it replied that:

    This domain is simply being used to identify the servers in our network, which involves a 'reverse DNS lookup' (the process that determines which domain name corresponds to which IP. This system is also used by anti-spam services to verify email addresses or to check that the network is working as it should.

This does not explain why Alexa is able to monitor it. Alexa is an Amazon service that sees the traffic for users who install its bars on their browsers.

Many are the Google services that interfere with this domain, such as Google Chrome's "private browsing" or Youtube.

---

Google takes advantage of reverse DNS resolution thanks to its 1e100.net domain...

Many of us would like to know what entries in DNS such as par03s03-in-f2.1e100.net mean.

Thanks to this, Google can know indirectly when my computer is connected to the internet thanks to the Google applications I have installed (e.g. Google Update/Installer, etc...).

The legitimate Windows service SRVCHOST.EXE queries the Google DNS even if we do not have Google DNS servers (8.8.8.8) thanks to the reverse resolution request because some of the applications installed and running on my computer at startup request the name for a Google IP address for some purpose. Same as 90% of the applications downloaded from the Internet...

On user claims:

    The service is used for geolocation.
    Google spies on users across this domain.
    For example for madrid the following is generated:

    mad01s15-in-f2.1e100.net
    mad01s08-in-f15.1e100.net
    dfw06s26-in-f15.1e100.net
    mad01s09-in-f24.1e100.net

    Etc.

    You can check it with netstat on cmd.

    Google keeps spying on people. Q