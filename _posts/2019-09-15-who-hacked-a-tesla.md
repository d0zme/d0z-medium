---
title: How a hacker gained control of a Tesla Car
layout: post
image: https://i.imgur.com/xjdrUyO.jpg
permalink: /hacked-tesla-car
---

A few years ago, a hacker managed to exploit vulnerabilities in Tesla's servers to [gain access and control over the entire fleet of the car manufacturer](https://electrek.co/2020/08/27/tesla-hack-control-over-entire-fleet/). Fortunately, it was a white-hat hacker who demonstrated the importance of this type of specialist and who has now explained the case.

Tesla enthusiast Jason Hughes had already received a $5,000 reward for reporting a vulnerability to the company that has revolutionized the automobile industry with its electric and connected approach.

Knowing that his network was not the safest, he decided to seek more rewards for mistakes. After some searching, he managed to find a lot of small vulnerabilities. "I realized that some of these things could be chained, the official term being a chain of errors, to gain more access to other things on his network. Finally, I managed to access a kind of server image repository on their network, one of which was Mothership," the name of Tesla's home server used to communicate with their fleet of clients.

Any kind of remote command or diagnostic information from the car to Tesla goes through Mothership. After downloading and analyzing the data in the repository, Hughes began using his car's VPN connection to attack Mothership. He finally landed on a developer network connection. That's when he found a bug that allowed him to authenticate himself as if he came from any car in the Tesla fleet.

"All he needed was a vehicle's VIN number, and he had access to all of them through Tesla's "tesladex" database because of his complete control of Mothership, and he could get information about any car in the fleet and even send commands to those cars. Hughes couldn't really send Tesla cars driving around? but he could 'call' them up and control them.

The hacker reported his findings to Tesla and the company awarded him a special reward of $50,000, several times his usual maximum, and used the information provided by Hughes to protect his network.

Electrek has published an annotated version of the bug report and described it as "a good example of the importance of white-hat hackers". Imagine if the vulnerabilities had fallen into the hands of cyber-crooks.
