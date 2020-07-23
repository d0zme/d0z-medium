---
title: Linus Torvalds approved the replacement of some terms in Linux code with neutral names
layout: post
permalink: /linux-torvalds-neutral-names
---

On July 10, 2020, [Linus Torvalds approved the need to replace some terms in Linux code with neutral names](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=49decddd39e5f6132ccd7d9fdc3d7c470b0061bb). In addition, most Linux kernel developers had agreed a few days earlier to this procedure for introducing new inclusive terminology.

After the third revision of the text on the use of inclusive terminology, which was approved by 21 well-known Linux kernel developers, a request was sent to Torvalds to include these changes in the Linux kernel version 5.9. But Linus ended up believing that there was no reason to wait for the next change acceptance window and accepted the new document already in the Linux kernel 5.8 branch.

Agreed alternative terms for replacing the master / slave pair, depending on the context, with pairs:

- primary / secondary;
- main / replica or subordinate;
- initiator / target;
- requester / responder;
- controller / device;
- host / worker or proxy;
- leader / follower;
- director / performer.


Coordinated term alternatives for replacing the whitelist / blacklist pair depending on the context with pairs:

- denylist / allowlist;
- blocklist / passlist.


It is currently assumed that this renaming should only be applied to the new Linux kernel code 5.8 or older, and to the documentation associated with this new code. However, the developers do not rule out that part of the existing code will also be affected by this renaming process in the future. There is now a process of further discussion and agreement on this procedure.

Earlier in July 2020, the Linux kernel developers mailing list began to actively discuss the need to replace some established terms with neutral ones in the code in order to keep up with current global trends and changes that developers of other projects are already introducing or planning to introduce. At that time, there were already several Linux kernel developers, including members of the technical board of the non-profit consortium Linux Foundation. Only two developers, James Bottomley and Stephen Rothwell, were opposed to this renaming process at the time. They suggested ignoring the topic, and believed that all these actions to replace certain terms in the code were essentially meaningless, since they were outside the scope of development and mainly concerned historical events, which are now accepted and burdened in society on the one hand only.
