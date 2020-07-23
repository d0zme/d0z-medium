---
title: Diablo 2 Redvex
layout: post
tags: diablo
---

# RedVex FAQs:

## Redvex Core Issues

- Where can I download Redvex?
  [Download Redvex from here.]()
        
- I get "Invalid SDK Version" error.. How do I fix this?
   [Go here to fix this.](https://web.archive.org/web/20090201225034/http://redvex.d2help.com/viewtopic.php?f=2&t=2316)
        
- I get "Error: Unable to bind on port 6112." over and over again in the Redvex window."
   To fix this (See Screenshot) Image do the following:
            - Either restart your computer (Easiest fix, if you're a newb). Or
            - You have two Redvex exe's loaded. Odds are the first Redvex is hiding in the bottom right hand corner of your computer in that system tray. It will look like a little red oval (Portal). Right click it, and select Quit. If you cannot see the red portal, you need to fist click the "Expand System Tray" button, which should look like a < (Less than) symbol. Then right click the portal, and select quit. Then when you go back to your other Redvex window, you can select Stop and Start. You may not even need to do this.. You already have Redvex running, so just close the new window, and load Diablo like normal, and you'll still be running Redvex.
       ![](https://web.archive.org/web/20131211073408im_/http://img171.imageshack.us/img171/8006/unable2bindww3.th.jpg)     
            
- Does "Loaded plugins (0 total, must have SDK version x or lower)" show up and you have installed plugins?
            You have not installed the plugins correctly, see Installing RedVex plugins or you are using a RedVex 2.5 plugin (found in the Older plugins forum) with RedVex 3.1 or the other way around.
- I only get "Accepting connections on port 6112..." and nothing happens in game, is this normal?
            Make sure you have created and are selecting the correct Realm server.
- I get this in RedVex log "Error: Unexpected Client PacketID Encountered: 0x...", what is this?
            You are not using RedVex with Diablo II 1.11 or newer patch
            You may not be using redvex 3.2 many problems related to this were fixed in that update
- I only get "Loaded plugins (0 total, must have SDK version 1-3 or lower)", I can't seem to make plugins show up, what did I do wrong?
            You must unzip the plugins. Some of them are in the .rar format. Use Win-Rar to unpack them. You must place the .dll files in a "Plugins" folder (If there is no .dll files you must give unzipping another try). If this folder doesn't exist, make it! Also make sure you are using the plugins with the right version of RedVex.
- What is the source folder? And what are this files within?
            Source Code is the code used to compile the programs. It has no value for you unless your are a programmer or plan to learn programming. You may just delete these files. (.cpp, .h, .pas, .dfm, .vcproj, .dpr)
- How can I bridge (run both at the same time) Redvex 2.5 and 3.2?
                Redvex 2.5 Settings
                    Server Settings
                        Logon Server: Choose one
                            uswest.battle.net
                            useast.battle.net
                            asia.battle.net
                            europe.battle.net
                        Port: 6112
                    Proxy Ports
                        Chat: 6113
                        Realm: 5001
                        Game: 4001
                RedVex 3.2 Settings:
                    Server Settings
                        Name: localhost
                        Chat Port: 6113
                        Realm Port: 5001
                        Game Port: 4001
                    Client Ports
                        Chat: 6112
                        Realm: 5000
                        Game: 4000
 - How can I restore Diablo II realms?
            Download this:
            RealmRestore.zip
            Extract it and double click on RestoreRealms.reg. Answer Yes on the question you get. The next time you start Diablo II your realms will be restored.
 - What does Game Server Logon Denied (42,43,44) mean?
            Unable to join due to game being full or wrong password.
---

RedVex is a Diablo II proxy with plugin support originally written by FooSoft. The plugins reside between the game client and Battle.net, allowing for full control over network traffic (packet modification, injection and filtering). This allows for a very safe and effective means of gameplay enhancement.

View the RedVex version history.

Image
Latest Version:

    Version 3.0.2 (February 25th 2008)
    Redvex_3.0.2_2-25-08.rar
    (Mirror 1)(Mirror 2)



Older Versions:
Version 3.0.1 (November 28th 2007)
Redvex_3.0.1_11-28-07.rar
(Mirror 1)


Version 3.0 (June 12th 2007)
Redvex_3.0_6-12-07.rar
(Mirror 1)


Version 3.0 (May 26th 2007)
Redvex_3.0_5-26-07.rar
(Mirror 1)


Version 2.6 (Beta 3)
Redvex_2.6_Beta3.rar
(Mirror 1)


Version 2.5 (Major Build)
Redvex_2.5.rar
(Mirror 1)


Version 2.1 (Minor Update)
Redvex_2.1.rar
(Mirror 1)


Version 2.0 (Initial Release)
Redvex_2.0.rar
(Mirror 1)
You do not have the required permissions to view the files attached to this post.

Zoxc	
    RedVex Developer
    RedVex Developer
     
    Posts: 191
    Joined: Fri Jun 15, 2007 6:59 pm

Top
RedVex Version History:

Postby ario on Fri Feb 29, 2008 6:06 pm
Changelog:

    Version 3.0.2 (February 25th, 2008) by Kingsob
        Added Criticalsection Lock/Unlock in tcpproxy this hopefully will fix unknown packet problems.
    Version 3.0.1 (November 28th, 2007) by Evan
        Added a new Packetflag: Visible
    Version 3.0 (June 12th, 2007) by Zoxc (?)
        Changed the default ports
    Version 3.0 (May 26th, 2007) by Zoxc (?)
        Fixed a game server/client mixup
    Version 2.6 Beta 3 by Zoxc
        Split the core in a .dll (Proxy) and a .exe (Controls/Interface)
        New user interface
        A toolbar extension system
        Loading/Unloading of plugins while proxy is running (Don't load plugins while already connected to Battle.net!)
        You can now change server ports (So you can use it with RedVex 2.5 on the same machine)
        RedVex can't run unless it's renamed and patched
        Added a wizard to configure RedVex
        Fixed GetPeer()
        Added menu items will not be hidden
        New plugins structure. Old plugins will NOT work!
        Support for other compilers than Visual C++
        Added a "Patch" program to kill checksum checks. Please drop RedVex.exe on it!
    Version 2.5 by Foosoft
        RedVex now minimizes to system tray
        Added -plugins, -settings, -nosettings, -start (see readme)
        Optional FreeGameModule()/FreeChatModule()/FreeGameModule() plugin exports for custom module instance release (otherwise they get deleted as in previous versions)
        IProxy::GetPeer() allows access to the peer proxy (chat/game and chat/realm matching)
        Added links to official homepage and IRC channel in help menu
        Bumped SDK version to 2
        Misc fixes
    Version 2.1 by Foosoft
        Implemented window class name randomization and removed mutex object check (for increased protection)
        Much more detailed status output
        Support for color customization in main window
        Fixed annoying bug with plugin directory search
        Various minor tweaks and bugfixes
    Version 2.0 by Foosoft
        Initial Release (?)
