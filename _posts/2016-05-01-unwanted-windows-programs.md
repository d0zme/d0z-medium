---
title: How To Prevent Unwanted Windows Programs From Loading At System Startup
layout: post
tags: windows
---

We all have them in our system tray, programs that load up and use precious memory resources and take up valuable space on your taskbar. Some of them you need, but most you can do without. Take charge and clean them out.

Some of the kinder and well written programs are configurable and allow you to change the settings that starts them up. If this option is available, then this is the best approach.

There are, however, many programs that do not give you the choice and no matter how many times you remove them, they return. Two that I find really annoying are the "Windows Messenger" and the "Quicktime Task". Both sit in the system tray and I don't need or want them there. I'll show you how to get rid of them forever if you have Windows XP Pro or Windows 2000. For those with Windows XP Home, this solution will not work.

First and foremost, however, I'd like to discuss a little gem of a program called Startup Control Panel, written by a young chap called Mike Lin from Boston. The program is available as freeware from www.mlin.net and Mike takes donations from those who want to contribute to his efforts.

This program works under all versions of Windows and is a vital part of any Windows installation. It's a program that will allow you to control exactly what programs load at system startup. This is one of the first things I install after setting up a computer with Windows. The program can either be loaded as a standalone program or incorporated into your Control Panel. I prefer the latter, but both work equally well.

When you invoke the program, there are a series of tabs across the top. The 4 that you should be concerned about are labelled, "Startup (user)", "Startup (common)", "HKLM/Run" and "HKCU/Run". These represent 4 different methods by which your computer can run programs when the system first starts. There are 3 other tab, which are not as important and are self-explanatory anyway. Note that the tabs may be on 2 levels depending on the windows size. I usually drag the window and make it wider so that all the tabs fit natly across on the page in a line.

Going through each of the 4 tabs, look at the checked items that will run. To stop them from running, uncheck the box. If you are unsure about a program, uncheck it and see what the effects are. You can awlays revise this later if something stops working. As an exercise, run the Windows Task Manager (by hitting the Ctrl, Alt and Del keys simultaneously) and note down how much memory is taken up by your system on a fresh start. The figure is listed on the status bar of the Task Manager under "Mem Usage". After unchecking all the unwanted programs, restart your system and compare the number and see how much less memory is being used. This is the amount you have saved and all things going well, you'll notice that your system is snappier and definitely less cluttered.

You will soon find that some programs do not like being unchecked. Yes, you guessed it, the two that I mentioned above, "Windows Messenger" and "Quicktime Task". They will reappear everytime you delete them. Worry not for there is another way for those running Windows 2000 or Windows XP Pro on the NTFS File System.

The NTFS File system comes with security built-in meaning that access to files, folders and programs can be limited. This is precisely the method which we will use to stop these pesky programs from loading.

Open up a Windows Explorer window and navigate to where these programs reside. For "Windows Messenger", it should be in your "C:\Program Files\Messenger" folder and is called "msmsgs.exe". Right click on the file and click on the "Security Tab". The security settings will show. Basically you want to apply the "Deny" access for all users and administrators. Do this by selecting each group and then clicking on the "Deny" checkboxes. When finished, click on the OK and you're done. The next time you restart the system, this program will be denied access to run. There are many who will rightly point out to me that there is an easier way to do this and that is to run Windows Messenger, navigate to the Tools menu and turn off the startup option. I have done this in the past but find that when a service pack or patch is loaded, that this program sometimes notoriously starts up again, so the Deny option works permanntly. Windows Messenger is a useless program and is superseeded by the MSN Messenger program.

Repeat the same for the Quicktim Task program which you can find by doing a search for "qttask.exe". You should find it in the "C:\Program Files\Quicktime" folder.

You can deny access to any program that you don't want to run. This is a powerful method of controlling your environment. It can be reverted by unchecking the Deny boxes at any time.

For those running Windows XP Pro, by default the Security system is disabled. This is easily fixed by opening up "My Computer" and selecting "Tools, Folder Options, View". The item either last on the list or close to last on the list will read something like "Use Simple File Sharing (Recommended)". Uncheck the box and click OK and your system will now have full security settings on all file or folders. The properties window of any file will then have the "Security" tab.

There is also the possibility that you have a Windows XP Pro system running the FAT32 file system instead of NTFS. The FAT32 file system does not have the in-built security of NTFS and will not allow you to allocate Deny permissions on files, folders or programs. You can however, easily convert the FAT32 file system to NTFS though using tools in XP. To find out how, do a Google search for "convert FAT32 to NTFS".

I wish you all the best with your computing experiences.
