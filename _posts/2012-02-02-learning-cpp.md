---
title: Want to Learn C++? 
layout: post
tags: programming
---

The first question you need to ask yourself is, "do I have the patience to learn?" Programming can be very frustrating, take vast lengths of time, and give you many unexpected errors along the way. There will be many points in time where you might need to ask others questions in order to complete your project, be prepared to never get a 'straight answer.' It is highly important that you research your problem, try rewriting your code segment another way, and put forth a valiant effort to solve the problem yourself. If you do have to ask others, be sure to include all the relevant information, be polite, use proper grammar, list the many steps you (should) have tried already, and try to keep it generally short as not many enjoy the intimidation of a wall of text and you will have a much greater chance of getting some help with your issue.

Just a few things you should be aware of, by no means complete...


## The Purpose of Learning.

What in particular made/makes you want to learn the language? 

Hopefully not for the sole purpose of hacking a game. While this reasoning is sound to spark interest, it is in my opinion a faulty way to start. Starting this way really hinders you, leading to bad habits which leads to bad code. This is because you basically jump into something that you don't understand, and working backwards tends to be harder then the appropriate way.

Patience is key.
    
It is a fact, you will hit a "brick wall" at some point and it is important not to let it dishearten you. Your life will be filled with compiling errors, memory issues, and the need to read seemingly endless amounts of information to resolve your issues. With every struggle you endure, you will come out the other side with something learned which adds to your arsenal of knowledge.

It will harm you in the long run to skip ahead.
    
It is important not to jump too far ahead of yourself, until you have a tight grasp of understanding on your current topic. Jumping ahead tends to lead to bad habits and sloppy code resulting in memory leaks or UD. (Undefined Behavior) Here is an example of UD in a win32 console application...
    
    Code:	

    #include "stdafx.h"
    #include "windows.h"
    #include <iostream>

    int main()
    {
      int X = 10;    // Declare the variable X, with the value of 10
      int Y;           //Declare the variable Y
      std::cout<< X+Y;    //Prints the result of X+Y to the console window
      Sleep(10000);   //Sleep for 10 seconds

    return 0;
    }

The line which prints the result of X+Y, will cause UD as Y is uninitialized . Because the variable Y is trying to be calculated when it has no assigned value, it will cause unpredicted results.


Take the time to really comprehend your code.

One of the biggest mistakes that you can make, in my opinion, is once you have something functional, moving onto something else. Does it work? Yes. But do you know why and how it works. It makes a monumental difference later on knowing how something works, rather then "I know this peice of code has to go here for my project to work."

After you learn something, try to refine it.

Once you learn something and have a fairly good grasp on it's usage, take a moment to stop and refine it. Is this the best possible way to implement this? Could this be shorter or clearer? Is this memory efficient? It is really tempting to jump to the next subject, but refining what you learn helps form a stable base of knowledge you can build upon.

## Getting your IDE setup and preparing to start learning.

You will need a compiler or an IDE containing one to build your projects. I personally use VC++ 08, but there are others to choose from depending on your project, preferences, or what it is your trying to accomplish. For the sake of simplicity and compatibility, i've listed the links below to get your IDE setup. Depending on what your making, you may need to download particular libraries from Microsoft. Once it is installed, you'll probably have to validate and register your copy which is free, only takes about 1 minute, and should be promted after installation or upon opening it for the first time.

![](https://web.archive.org/web/20111002041252im_/http://img38.imageshack.us/img38/9194/vsecppheader.jpg)

Microsoft Visual C++ 2008 Express Edition
http://www.microsoft.com/Express/vc/

Here is a step by step guide for installation. You should be fine, but this could be helpful if you run into any trouble.
http://cplus.about.com/od/learnc/ss/vc2008_2.htm

## A Starting Point...

There are thousands of tutorials all over the internet, but I do have a bottom of the totem pole starting point for you that will get you making small applications within a few hours. It is a series of YouTube videos, explaining many beginner aspects, from using your IDE to actual programming. It is called Absolute n00b Spoonfed C++. It truly is spoonfed, and sometimes the guy might drag on abit on a particular subject but i'd suggest sticking with it as it probably is the best "hands on" introduction to the language for total beginners. You should begin with video (1), obviously...

http://www.youtube.com/profile?user=antiRTFM&view=videos&start=40

antiRTFM YouTube Channel (By the way, RTFM = Read the fucking manual, which is a common response to beginners.)

