---
title: Ignoring the Great Wall of China
layout: post
---

I wanted to post again about the great Chinese firewall.Â  Apparently someone had the same idea that id and I had around ways to get around the filters.Â  Apparently, according this post on bypassing the Chinese firewall, it uses RST packets when it sees the forbidden content pass over it’s firewalls.Â  The RST packets are sent in either direction. However, if your firewall is set up to ignore RST packets AND the person in China is also set up to do the same, the text will flow through the firewall indisciminately.

However, this isn’t filter evasion, as the flag will still be there (and theoretically could be much worse because it will continue to send RST flags over and over and over for every request you make with the forbidden content in it).Â  So, without having someone in China to test this theory, it’s hard to do, but it is believed that it will work.Â  Interesting theory, anyway.Â  If anyone has some equipment in China that would like to help us test it, it would be a fun experiment (especially for id, I know).
