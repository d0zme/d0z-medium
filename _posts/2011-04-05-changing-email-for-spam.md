---
title: Changing Email Addresses For Spam
layout: post
tags: email
---

While looking back at some of my old speeches, and after writing the last blog post it occurred to me there is another attack I haven’t heard anyone talk about. Often times spammers will use contact member forms for spamming purposes. But most contact forms can’t spoof the contact name so this form of spamming is pretty limited. However, let’s consider another common scenario, which is that a user is allowed to change their email address. Almost never is there an email address confirmation link sent to make sure you are indeed the owner of the email address. So let’s take an actual example.

Let’s say Cathy wants to spam Alice, but Alice isn’t a member of the message board. Cathy signs up with two accounts, one to send messages from and one to receive them. Cathy logs in as the second user account and changes her email address to Alice’s. She then logs into the first user account and send the spam, which then gets routed to Alice. Then Cathy logs in to her second account, switches it to the next spam victim, logs back into her first account and sends a second spam and so on.

The limitations here are that the email must actually contain the spam message to work, so if it’s just a link back to the platform, that won’t suffice since Alice isn’t a legitimate user of the system, let alone has access to Cathy’s account. The second problem is that the email probably contains some site specific information which can easily identify the spam as such. And thirdly, many sites send an email change notification to alert users that their email has been changed, so when Cathy switches her address over and over, she will also inadvertantly be sending emails to her victims telling them that she’s switching accounts.

But in this way I believe many existing member to member communication functions can be used as spam gateways. Weird, huh?
