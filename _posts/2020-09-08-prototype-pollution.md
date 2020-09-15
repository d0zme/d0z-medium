---
title: Don't Underestimate Prototype Pollution
layout: post
image: https://i.imgur.com/FlbQ2MX.jpg
permalink: /prototype-pollution
---

Although in some places they speak of [prototype pollution](https://codeburst.io/what-is-prototype-pollution-49482fc4b638?gi=6d2fa3d51132) (or 'prototype comtamination') as a new technique for attacking websites. In reality, this novelty is relative, since as early as 2018 it is possible to find some CVEs, such as this one that affected lodash. It was more notorious when, last year, a similar problem was detected in jQuery. What was not so much mentioned at the time is that it was actually the second incidence of the same type, and that the previous one had taken place three years earlier. Therefore, and in view of the dates, we are actually talking about a problem that has been identified for quite some time.

If you don't know this, you should know that Javascript is based on using inheritance, so that when a new object is created, it acquires the properties of the model on which it is based, which is the prototype, by default. Obviously, at the time when, either during development or at runtime, specific values are assigned to those properties, the ones inherited from the prototype are removed. The fact that the new object does not come "empty", and that the developer can use the prototype to make adjustments only once, and not for every object, brings quite a lot of agility to the development.

The problem with prototype contamination is that a malicious actor can avoid attacking a particular object in the code and instead target the prototype, on which it will focus its efforts. And it makes perfect sense, because the modification of the object can have a limited scope, while the modification of the prototype provides a more global scope, as it reaches all objects that are inheriting properties from it.

And prototype contamination, if undetected, offers another advantage over modifying objects individually, and that is that the inheritance of the object's properties will apply not only to existing objects, but also to those that may be added in the future. As long as the prototype remains contaminated, all objects, present and future, will be compromised by this problem.

We are not talking about a particularly new attack technique, since the injection of code has been around for many years. The particularity of prototype contamination is that it affects a very specific context, Javascript development frameworks. Furthermore, until 2018, and even in some discussions in 2019, it was doubtful whether this was a security problem affecting only the frontend (clientside) or, on the contrary, could also have effects on the backend (serverside). This has meant that, despite being a very serious threat, it has been underestimated, falling somewhat under the radar.

At this point, however, there is no longer any doubt about the impact that prototype contamination can have on the server side. It has been proven, for example, that prototype contamination can be used to carry out a denial of service attack based on NodeJS, another popular Javascript framework.

With regard to solutions, and given that the attack is carried out on the client side, one of the main recommendations is to limit the user's entry possibilities as much as possible. Establishing strict limits on which objects can be modified by users is currently the main way to combat the risk posed by prototype contamination. Other options, such as individual review of all types of objects that can be compromised, escape (by volume of work) the vast majority.
