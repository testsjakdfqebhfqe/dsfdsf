---
title: GUI Setup Utility
excerpt: Optional setup utility that makes setup a breeze.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This graphical utility can be optionally used by end-users to configure a Control D [Device](doc:devices) with 2 simple steps. Using this tool skips all the manual configuration steps and makes setup a breeze. 

# Download

It's recommended you use the web tutorial part of the setup flow. It will prompt you to install the app when needed. Or you can download them below:

* Windows (AMD64) - [https://assets.controld.com/utility/controld\_x86.exe](https://assets.controld.com/utility/controld_x86.exe)
* Windows (ARM64) - [https://assets.controld.com/utility/controld\_arm.exe](https://assets.controld.com/utility/controld_arm.exe)
* MacOS (Intel) - [https://assets.controld.com/utility/controld\_x86.dmg](https://assets.controld.com/utility/controld_x86.dmg)
* MacOS (ARM) - [https://assets.controld.com/utility/controld\_arm.dmg](https://assets.controld.com/utility/controld_arm.dmg)
* Android - [https://play.google.com/store/apps/details?id=com.controld.setuputility](https://play.google.com/store/apps/details?id=com.controld.setuputility)
* iOS - [https://apps.apple.com/us/app/control-d-quick-setup/id1518799460](https://apps.apple.com/us/app/control-d-quick-setup/id1518799460)

# Create a Device

Go into the Endpoints section, and [Add an Endpoint](https://controld.com/control-panel/filters?deviceDialog=platform\&overlay=profile-management) for the appropriate platform. If you're using Free DNS resolvers, click on "Setup Guide" button. 

# Get Configuration Code

The **Resolver ID** is the configuration code you're looking for. 

<Image align="center" width="55% " src="https://files.readme.io/c9a97b16b3ea67e0e9bbd6572c225e87066d4e49834e338a0550cad20425c2bb-iOS_Endpoint_Resolver.png" />

If you don't have the app installed yet, click **Help Me Configure > Automatic Setup** button.  You will be presented with this screen. 

<Image align="center" width="55% " src="https://files.readme.io/3fd1c2b323985935ec4bf41595513105ed4b82ec8aa00614b4f1264f6b9ccf8d-iOS_AutoSetup.png" />

From here, you can download the utility app. 

# Paste Configuration Code

Paste the configuration code (Resolver ID) into the box of the app you just downloaded and launched. The interface looks similar on all supported platforms. 

<Image title="util.JPG" alt={1906} align="center" src="https://files.readme.io/670c1f657a8e35be155fede12b90e088b88c5adab490cfdbde5a1364fc70aa59-Gui_Config_Not.png">
  This illustrates the Windows version, however MacOS, Android and iOS look virtually identical.
</Image>

That's it, once you see a **Configured** message you're done here. The utility can be closed. Control D will run silently in the background (even after reboot), and use the DNS resolver associated with the device that was configured.

To verify that your system is configured correctly, you can go to the [Status Page](https://controld.com/status). 

## Modes

Depending on your OS, the Settings menu allows you to choose between up to 2 configuration modes. 

* **Managed** (Default) - This mode uses [Command Line Daemon](doc:ctrld) under the hood, to enable DNS-over-HTTPS using an installed system service. This will work in every operating system.
* **Native** - Configure DNS-over-HTTPS natively if your OS supports it (Windows 11, latest MacOS)

We recommend you use the Managed mode, which is the default. 

# Uninstall

To remove the Control D resolver from the device, simply start the downloaded utility again (or download a new version) and press "Disable Control D" button.
