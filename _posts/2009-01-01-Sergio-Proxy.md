---
title: Sergio Proxy
layout: post
image: 
tags: source code
---

So after a ridiculously long period of procrastination, I finally got around to updating Sergio Proxy to make it remotely usable. I was never very happy with how the initial code turned out, but given that it was hacked out in a couple days just to test some ideas, I suppose that shouldn't be surprising. My original hope for it was to provide a very easy to extend plugin interface that allowed Python programmers to easily modify requests and responses during a MITM attack on HTTP.  While you could extend it without too much trouble, it was far from perfect, and passing options to the thing was an atrocious mess. Worse, my hooks into Twisted weren't the most stable or fast, rendering it not very useful.


I believe I've solved some of these issues in this release, although you can certainly judge for yourself. I've made three major changes: first, rather than using my own transparent proxy classes for interacting with Twisted, I've instead started using Moxie Marlinspike's sslstrip to provide the proxy functionality. 


Although I didn't know it when I first started Sergio Proxy, sslstrip uses almost exactly the same method for creating the transparent proxy: extending the Twisted framework's HTTP proxy classes. 


Rather than duplicate effort to create something that would still be miles behind, I instead decided to focus on providing a convenient plugin interface that could hook sslstrip at various points during operation. This brings me to the second change: a new plugin interface that should make it ridiculously simple to extend Sergio Proxy. I've currently implemented three modules (SMBAuth, ArpSpoof, and Upsidedownternet), but really there are tons of other things that could be done. Finally, I completely revamped the logging and options code, which were virtually non-existent in my first release. Combined, these should make Sergio Proxy a nice framework for making use of HTTP MITM attacks. You can grab the new code here: https://code.google.com/p/sergio-proxy/downloads/list


 Edit: I've also added a simple BrowserPwn plugin now, grab the current trunk to get it: https://code.google.com/p/sergio-proxy/source/checkout
 
## Using Sergio Proxy

So enough about the changes: how would one go about using it? Well, if all you want to do is evoke an SMB authentication attempt or launch the Upsidedownternet, just run sergio-proxy.py -h and choose your desired options. ArpSpoof will set up the MITM if you so desire (requires ettercap or arpspoof), and sslstrip will record what it normally does. If you want to do something else, though, you'll need to create a new plugin. Don't worry, it's quite simple!


First, you need to do a few simple things. The provided plugins provide good examples, but I will step through the required steps just in case. All plugins inherit from the Plugin class in plugins/plugin.py, and Sergio Proxy needs to know the subclass relationship, so you must do a "from plugins.plugin import Plugin" in every plugin file. No exceptions. Then, you need to define some class attributes to tell Sergio Proxy about your plugin. These are as follows: name (human friendly name), optname (option name to enable plugin), has_opts (needs to add opts to argparse object), and implements (a list of hooks it implements). If you require arguments, you need to implement the add_options function. It takes an argparse Parser object as its only argument, where you can then do with it as you please. Be warned, though: if your arguments conflict with others, you may have issues.


Now, you are ready to implement the actual functionality of your plugin. There are 5 functions that really matter, and you can see them in the base Plugin class: initialize, handleHeader, connectionMade, handleResponse, and finish. initialize is passed the namespace that argparse parsed, and is called whenever your plugin has been enabled by a command line switch and is going to be run. You should do any setup you require here rather than __init__, as you won't have options in __init__ and it entirely possible your module won't be run after that point. finish, likewise, is called on shutdown.


There are three points where Sergio Proxy hooks sslstrip by default right now: on connecting to the server prior to sending the victim's request, on receiving any header from the server, and prior to sending a response to the client. These functions are the other three functions I mentioned. It is quite simple to add more if necessary, but that's outside the scope of this post. Whenever sslstrip hits any of these three points during execution, Sergio Proxy checks to see if any plugin wants to hook that function and, if so, calls the function with arguments that were provided to the function call in sslstrip. Generally,  if you have changes you want to send back to sslstrip, you should modify the request object, and not return anything. However, in the handleResponse hook this is not possible (as the local var data is used rather than an object attribute), and you must return a dictionary containing the modified arguments. This is currently the only case where this is necessary, but it's important to note.

Now, all you need to do is override these functions to do what you want. If you're wondering what information you have access to through the request object, it may be useful to either a.) hook the function you want and print out information about it at that time or b.) look through sslstrip and the Twisted proxy documentation. Also, the plugins I provided show some of the basic things you might want to do.

Hopefully you all find the new changes useful. If you end up writing a plugin, please feel free to submit it! If it was useful to you, it is likely it will be useful to others as well.
