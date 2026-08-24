---
title: MacOS
excerpt: How to configure Control D on any MacOS computer.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
# Automatic Setup (GUI)

Want to spend the least amount of time setting up Control D on a MacOS device? We probably read your mind. 

[GUI Setup Utility](doc:gui-setup-utility) is what you're looking for. 

# Automatic Setup (CLI)

GUI is not your thing, looking to do a scripted deployment, or have an existing MDM profile already in use? Have no fear, there is an app for that. 

[Command Line Daemon](doc:ctrld) is what you're looking for.

# Manual Setup (Profile)

It's entirely optional to use the above applications, and you can manually setup an Apple DNS Profile that will enable DNS-over-HTTPS system wide. In order to do this, follow the Manual Setup guide in the Web Control Panel after you create a MacOS device (or view an existing one). 

In **Step 1** of the **Manual Setup** you will be asked to download a signed .mobileconfig profile. You can optionally customize this DNS profile to exclude networks where Control D should not be used, as well as exclude specific domains you wish to be bypassed from Control D. This is helpful to make captive portals work. 

![3574](https://files.readme.io/5734ebc-macual_mac_profile.JPG "macual_mac_profile.JPG")

# Google Chrome Warning

This section is only applicable if you use Google Chrome browser. 

> 🚧 Google Chrome Warning
>
> If you use MacOS Ventura along with Google Chrome, there is an OS bug you should be aware of, where Google Chrome will disregard your OS DNS resolver in some cases, making it bypass Control D. 
>
> The solution is to also configure your Device [directly in Google Chrome](https://blog.controld.com/how-to-set-up-control-d-on-google-chrome/).
