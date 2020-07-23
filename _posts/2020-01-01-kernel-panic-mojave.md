---
title: Kernel Panic on macOS Mojave
layout: post
tags: osx
---

Many Apple users have a complaint that after restarting their Mac they can see a message “Your computer restarted because of a problem”. This unknown error is known as kernel panic. Here I am going to tell you the solutions to fix this issue.

What is the reason for this issue?

Kernel panic issue occurs because of faulty software that installed on your Mac. This issue will continue until you find that faulty software.

# Solution 1: Disconnect third-party devices and uninstall third-party apps

- Make sure that your Mac has enough free space on the startup disc. Your Mac should have at least 20% of free space.
- Uninstall all third-party apps, plug-ins, and drivers.
- Disconnect all (third-party) peripheral devices like printer, scanner, mouse, keyboard, webcam, USB, FireWire, etc from your Mac.
- Then restart your Mac and check whether this problem occurred or not.

Note: After restarting your Mac, connect any one of the device and restart your Mac. When you reconnect each device, restart your Mac and find which one causes this issue.

# Solution 2: Restart your Mac in Safe Mode

Restarting your Mac in Safe Mode will fix many issues in the Mac. But you can’t use some features in Safe Mode.

- Press and hold the Power Button to turn off your Mac.
- Press the Power Button to turn on your Mac.
- Press and hold the Shift Key immediately after pressing the Power Button.
- You can see the Apple Logo on the screen. Don’t leave the Shift key when you see the Apple Logo.
- Keep pressing the Shift Key until you see the Login Window.
- Select your User Account and then enter the Password to login. You may need to login twice if FileVault is turned on.
- If your Mac successfully starts up, go to Apple menu->About This Mac->Software Update.
- Click “Updates” tab.
- Click “Update All”.

Note: If it doesn’t work out, leave Safe Mode and then try next solution. To leave Safe Mode, restart your Mac via Apple menu->Restart. Wait until your Mac restarts.

# Solution 3: Remove “IOVideoPocketCam.kext”

- Open Finder.
- Click Go->Go to Folder.
- Type /Library/Extensions and then click “Go”.
- Move the file “IOVideoPocketCam.kext” to Trash.

# Solution 4: Reset SMC

If your Mac has a non-removable battery,

- Shut down your Mac by pressing the Power Button.
- Press and hold the Shift + Control + Option + Power Button simultaneously.
- Then release the keys at the same time.
- Press the Power Button to turn on your Mac.

# If your Mac has a removable battery,

- Remove the battery out of your Mac.
- Press and hold the Power Button for 5 seconds.
- Insert the battery into your Mac.
- Turn on your Mac.

# SMC reset on iMac, Mac Mini, & Mac Pro

- Turn off your Mac.
- Disconnect the power cord.
- Wait for 20-25 seconds and then plug the power cord back in.
- Wait for 5 seconds and then turn on your Mac.

# Solution 5: Reset PRAM/NVRAM

- Press and hold the Power Button until your Mac turned off.
- Press the Power Button to turn on your Mac.
- Then immediately press and hold the Option + Command + P + R keys simultaneously as quickly as possible after pressing the Power Button.
- Keep pressing those keys until you hear the startup sound for the second time.
- Wait for some time. Your Mac may take 15-20 minutes to restart.
- Then your Mac will restart normally.

# Solution 6: Fix disk errors in Recovery Mode

- hold down the Power Button until your Mac turns off.
- Press the Power Button to turn on your Mac.
- Press and hold the Command + R keys simultaneously as soon as possible after pressing the Power Button until the Apple Logo appears.
- After that macOS Utilities window will appear with 4 options. Tap “Disk Utility”.
- Tap “Continue”.
- Select the disk/drive (Macintosh HD) that you want to repair.
- Select First Aid->Run. This action will check the disk for errors.
- Click “Done”.
- Close Disk Utility.
- Restart your Computer via Apple menu->Restart.

# Solution 7: Reinstall Mojave

- Press and hold the Power Button to turn off your Mac.
- Press the Power Button to turn on your Mac.
- Press and hold the Command + R keys simultaneously as soon as possible after pressing the Power Button.
- Keep pressing Command + R keys until the Apple Logo appears.
- After that macOS Utilities window will appear with 4 options. Tap “Reinstall macOS”.
- Tap “Continue”.
- You will be prompted to choose your hard disk/drive. If you are not asked to select your disk, tap “Show All Disks”. You may need to enter your Apple ID.
- Tap “Install”. Wait until the installation process is completed.
- Your Mac will restart after completing the installation.

If you know any other solutions to fix macOS kernel panic issue, let us know through your comments.
