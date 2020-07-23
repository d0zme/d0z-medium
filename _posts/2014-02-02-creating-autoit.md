---
title: Creating AutoIt Bots for Online Games
layout: post
tags: programming
---

I created this post because I want to suck up space and waste peoples time who read it, if you don't like what I have to say, just move on and ignore me hence-fourth, thank you.

Bots are created for generic routines for any game. I'll list examples (a couple):

- 1) Diablo II -- Chaos running, Baal running, "Magic Finding," etc.
- 2) RuneScape -- "Fishing," "Cutting trees," and "Cooking" to make higher skill levels.

If you're new to programming, AutoIt (a scriptting language) would be a great start.

The main things that you (I personally) use the most is:
- Pixel detection
- Mouse emulation
- Keyboard emulation
If you want to go a few steps further, you can use packets which I suppose would give you a faster/better reaction, for multiplayer games.

AutoIt can be found here: http://www.autoitscript.com/autoit3/

You can use AutoIt for just about every type of game, you can even use it for the most basic of things, for example:

The beginning of a game on StarCraft. Have AutoIt create an SCV instantly and have all SCVs mine individual mineral packs so they gather faster.
Or on Age of Empires, you can have it build a (pretty and) organized row of Houses, in a split second. Which I used to use VBS for that in 1998.
You could even use AutoIt to notify people you're about to create a game, and then have it create it -- It beats using a bot in a channel to tell everybody what game name/pass/number you're on.

The list can become endless, there are many repeditive things on games of every genre.

You could even use bots to beat games entirely without lifting a finger! Like The Incredible Machine (aka TIM), and Jazz Jack Rabbit.

If you're serious about wanting to learn how to make bots for games, pick the stupidest but most simple things.

Projects for people who are 100% new and want to create bots (Diablo II):
- Use AutoIt and have it spam "Welcome to" so and so's "runs!"
- Use AutoIt and have it drop X amount of gold repeatedly until you press a hotkey to stop.

Projects for people who are 100% new and want to create bots (RuneScape):
- Use AutoIt and have it click on a tree every X seconds
- Use AutoIt and have it create a fire every X seconds

It's the little things in life that make the best improvements.

AutoIt has a help file which explains nearly every command (with examples) in great detail. Very helpful.

---


#cs ----------------------------------------------------------------------------

 AutoIt Version: 3.2.2.0
 Author:         Danielle

 Script Function:
   To automatically reply to an Admin Message (web-based game) checking if I'm a bot. :D

### Example Code:
----------------------------------------------------------------------------

; Endless loop to keep the program running

While (1)

   Sleep(1000)
   
   ;; Checks to see if the window exists -- if it does, it activates it (puts it in focus, up front) and types text and clicks the OK button
   If WinExists("Edit post - ") Then
      WinActivate("Edit post -")
      
      ;; Click on the place to type
      MouseMove(600,600,0)
      MouseClick("left", 600, 600, 1, 0)
      
      ;; Type the message, wait a bit so it doesn't look suspicious -- You could randomize the time with a variable (within 10 seconds to reply)
      Send("Yeah, why?")
      Sleep(500)
      
      ;; Click on the send button! Presto!
      MouseMove(400,400,0)
      MouseClick("left", 400, 400, 1, 0)

   EndIf

WEnd 
