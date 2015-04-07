Context - This session is a discussion about managing Windows, using PowerShell, using DSC - hosted by Jeffrey Snover
Attendees - 17

How do I connect from a Linux environment to a Windows machine?
+ Copy files
+ SSH or WinRM?  SSH because it exists everywhere and the console is treated as local so I am not blocked from tasks such as Windows Update, and because it is not reliant on WMI which sometimes need to restart
+ Took a vote - SSH or WinRM as a way to connect from Linux to Windows?  90% SSH

I noticed a lot of Microsoft bloggers screenshot cmd instead of PowerShell

The biggest thing I miss on Linux, is PowerShell, because of objects and piping

There isn't a concept of PowerShell profiles in PS remoting? - We will check on this

Command line argument quoting - it is too difficult to pass complex character strings as parameter input
Many tools, many parameter implementations, this issue is very complex.  The workaround is --%.

PowerShell - file exits with 0 with failed scripts, however -cmd returns an error code

It is too easy to bury exit codes in a script where something crashed but then cmdlets were run after the crash and the script still returned exit 0

Need editing in console and remoting - emacs conventions - PSReadline helps a lot

Windows is too large so I can't easily move it to my test environment
+ What tasks?
  + It should run Chef
  + Package management
  + IIS
  + Networking stack
  + Differential copy utilities (Robocopy)
  + Volume management
  + Drive mapping to remove shares

There are restrictions around what can be run remotely in PS sessions.  Memory utilitzation especially.  The limits are much too low.

Double-Hop works fine over SSH, we can't do it over WinRM

Automating Group Policy is too difficult, I need to be able to apply settings to group policy rules, especially security rules, via PowerShell

Too many reboots!
  + Name change
  + Joining a domain
  + They take way too long

I can't push files to a Windows machine easily from a non-Windows environment

Containers for Windows - this can't come soon enough
  + The most important thing is quickly getting feedback on build test results

I need it to be ok for people like Vagrant to make Windows Images with their software included available for download

>>>  The Vagrant box from MSOpenTech needs to be updated.


Snippets

[1]
```PowerShell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.


PS C:\WINDOWS\system32> etsn -cn .
[localhost]: PS C:\Users\user\Documents> $profile |fl * -force
[localhost]: PS C:\Users\user\Documents> $profile
[localhost]: PS C:\Users\user\Documents> exit
PS C:\WINDOWS\system32> $profile
C:\Users\user\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
PS C:\WINDOWS\system32> $profile |fl * -force


AllUsersAllHosts       : C:\Windows\System32\WindowsPowerShell\v1.0\profile.ps1
AllUsersCurrentHost    : C:\Windows\System32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1
CurrentUserAllHosts    : C:\Users\user\Documents\WindowsPowerShell\profile.ps1
CurrentUserCurrentHost : C:\Users\user\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
Length                 : 78


PS C:\WINDOWS\system32> $profile.currentuserallhosts
C:\Users\user\Documents\WindowsPowerShell\profile.ps1
PS C:\WINDOWS\system32>
```
[2]
```PowerShell
PS C:\WINDOWS\system32> Get-PSSessionConfiguration

Name          : microsoft.powershell
PSVersion     : 5.0
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote
                Management Users AccessAllowed

Name          : microsoft.powershell.workflow
PSVersion     : 5.0
StartupScript :
RunAsUser     :
Permission    : BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : microsoft.powershell32
PSVersion     : 5.0
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote
                Management Users AccessAllowed


PS C:\WINDOWS\system32> Set-PSSessionConfiguration -Name microsoft.powershell -StartupScript
```

[View original notes in etherpad](https://e.chef.io/p/PowerShell), 