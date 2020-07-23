---
title: Ladder Slasher Bot Source Code
layout: post
tags: source
---

Simply find it here: http://www.mediafire.com/file/hmknj2ehzmn/LSbotsource_v1.19.rar/file

Don't forget to move ImageSearch.au3 to the AutoIt "Include" Folder.

Pretty much as the title says. Here is the source for a bot for version 1.19.0 of ladder slasher. It is written in AutoIt and uses one .dll (not injected)

Currently it fights solo in the arena and chickens when its health or mana gets low.
Uses charms or weapons to attack.
Places stat points automatically (if you want)
100% pixel based programming gives the user stealth.
Encrypts passwords and prevents users from copy/pasting in the input fields. So you can't just nab the password by looking through cfg.ini

Looting needs some serious love. Currently set up to loot via screenshot database. This would work and at a decent speed but like I said it needs some effort first. Basic script for looting included.

Everything is based off screen coords which shouldn't be an issue with the window positioning technique I've got in there.

The state of the ladder slasher game can be easily be acquired by simple image detection. Everything needed to make AutoIt search for images is included.

The full source code of ImageSearchDLL.dll is also included. It is not my .dll and many thanks and credits to the author(s). His/her/their credits are inside the source files.

---


If you want to test whether or not it works right picking up certain items then paste every image into one big *.bmp file and set it to your desktop.

Then use:

Code:

#include <ImageSearch.au3>
#Include <File.au3>
HotKeySet("{END}" , "_end")
HotKeySet("{INSERT}", "testscanforloot")
While 1
   Sleep(50)
   ToolTip("Press insert to look for images" & @CRLF & "Press ""END"" to quit", 0, 0)
WEnd

Func testscanforloot()
Local $x1, $y1
Local $lootqualscan = _FileListToArray(@ScriptDir & "\pics\item\", "*.bmp", 1)

For $cnt = 1 To $lootqualscan[0]
ToolTip("File: " & $lootqualscan[$cnt] & " " & $cnt & " of " & $lootqualscan[0], 0, 0)
Sleep(300)
If _imagesearch(@ScriptDir & "\pics\item\" & $lootqualscan[$cnt], 0, $x1, $y1, 120) = 1 Then
   MouseMove($x1, $y1, 0)
   Sleep(700)
   MsgBox(0, "Found image", $lootqualscan[$cnt] & @CRLF & "X=" & $x1 & @CRLF & "Y=" & $y1)
Else
   Sleep(700)
   MsgBox(0, "Did not find image", $lootqualscan[$cnt])
EndIf
Next
EndFunc

Func _end()
   Exit
EndFunc	
