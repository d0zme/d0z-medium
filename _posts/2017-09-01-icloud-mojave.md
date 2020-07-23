---
title: iCloud Contacts Not Syncing to macOS Mojave
layout: post
tags: osx
---

Many Apple users have a complaint that iCloud contacts not syncing to their Mac. They said that this problem occurred after updating Mojave. Here I am going to tell you the solutions to fix the issue iCloud contacts not working on macOS Mojave.

Before trying these solutions,

    Make sure that you are using the same Apple ID on all your Apple devices such as Mac, iPhone, and iPad.
    Make sure that your internet connection is good and speed.

Solution 1: Disable and enable Contacts

    Go to Apple menu->System Preferences->iCloud.
    Unselect the checkbox next to Contacts.
    Restart your Mac.
    Go to Apple menu->System Preferences->iCloud.
    Select the checkbox next to Contacts.

Solution 2: Rename the Address Book folder

    Quit the Contacts app.
    Open Finder.
    Click Go->Go to Folder.
    Type ~/Library/Application Support/ and then click “Go”.
    Rename the Address Book as AddressBook(old) or any name you want.
    This process will create a new AddressBook and it will also sync with your iCloud properly.
    Open the Contacts app. Now you can see all your iCloud Contacts.

Solution 3: Delete everything with AddressBook in its name

    Open Finder.
    Select Go->Go to Folder.
    Type ~/Library/Containers and then click “Go”.
    Find if there anything with AddressBook in its name and delete it.
    Likewise, do it for following commands: ~/Library/Application Support, ~/Library/Preferences, and ~/Library/Caches.
    Go to Apple menu->System Preferences->iCloud.
    Unselect the checkbox next to Contacts.
    Restart your Mac.
    Go to Apple menu->System Preferences->iCloud.
    Select the checkbox next to Contacts.
    Now all the contacts from iCloud will sync with your Mac. This process will take 5-10 minutes.

Solution 4: Sign out of iCloud and sign in

    Go to Apple menu->System Preferences->iCloud.
    Click “Sign Out”.
    If you want to keep any iCloud data on your Mac, select “ Keep a Copy” (or) unselect all checkboxes and click “Continue”.
    Go to Apple menu->System Preferences->iCloud.
    Sign in to iCloud using your Apple ID and Password.

Solution 5: Disable and enable iCloud Contacts on iPhone & iPad

    Open Settings->Apple ID (Your Name)->iCloud.
    Make sure that “Contacts” is enabled under APPS USING ICLOUD.
    Disable “Contacts”.
    If you want the contacts that synced from iCloud, tap “Keep on My iPhone”.
    If you don’t want the contacts, select “Delete from My iPhone”.
    Wait for few seconds and then enable “Contacts”.
    Select “Merge” in the pop-up box.

Solution 6: Restore Contacts from icloud.com

    Go to icloud.com.
    Enter your Apple ID and the click the arrow symbol.
    Enter your Apple ID’s Password and then click the arrow symbol.
    Select “Settings”.
    Select “Restore Contacts” under Advanced.
    Click “Done”.

If you know any other solutions to fix this issue, let us know through your comments.
