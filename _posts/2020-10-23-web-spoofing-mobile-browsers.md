---
title: Web address spoofing now feasible in mobile browsers
layout: post
tags: security
image: https://i.imgur.com/T9I15By.jpg
---

Hiding fingerprints is always a key point for cyber-crooks, which is why spoofing (hiding relevant identity elements) is a commonly used resource. Impersonating a legitimate identity is always a good technique, as it guarantees that the action is illegitimate by means of a reliable and trustworthy name. Spoofing can take the form of names, email accounts and web addresses, anything can be used to impersonate a trusted person, company or entity.

Thus, cyber-crooks are constantly exploring new techniques for spoofing, and researchers and security companies are constantly working to find security holes that can be used for this purpose. The latest example of this is an [investigation carried](https://blog.rapid7.com/2020/10/20/vulntober-multiple-mobile-browser-address-bar-spoofing-vulnerabilities/) out by Rapid7, which has identified a vulnerability affecting multiple mobile Web browsers, which allows users to modify the Web address displayed in the address bar.

The problem, which was reported by the browser managers, many of the experts have already solved it, it is supported by Javascript and a strange condition of the content shown in the address bar. This is because, under certain conditions, the browser can be forced to show a specific URL in the same, even though a different page is loading. This is particularly dangerous, because the user has no way of checking it unless they click on the address bar to make sure the page they should be loading is. Otherwise, the appearance will be that everything is going well.

Apple Safari and Opera Touch are two of the browsers affected by this spoofing problem. In the case of Safari, Apple claims to have already fixed the problem, while Opera claims that an updated and free version of this problem will be released on November 11th. Other affected browsers include RITS Browser, Yandex Browser, Bolt Browser and UCWeb. With respect to the latter two, there is currently no evidence that they will solve the problem, which is still present.

Research also found that the MacOS X version of Safari is vulnerable to the same bug. According to Rapid7 the problem has been solved in a Big Sur macOS update released last week. This is not the first time a vulnerability of this type has been detected in Safari. In 2018, a similar type of spoofing was revealed in the address bar that caused the browser to retain the spoofed address and load the content of the fake page thanks, also, to JavaScript.
