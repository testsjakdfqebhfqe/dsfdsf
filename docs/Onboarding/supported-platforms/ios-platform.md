---
title: iOS
excerpt: How to configure Control D on any iOS device.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Automatic Setup (GUI)

Want to spend the least amount of time setting up Control D on your iOS device?

[GUI Setup Utility](doc:gui-setup-utility) is what you're looking for.

# Manual Setup

Despite how daunting this may sound, setup on iOS is actually very easy. 

<Image align="center" width="50% " src="https://files.readme.io/57b3a293ad2b500ee55388d2607b840e7d7bd14e764dd58ae6a9ddf3ad005378-ios_help_config.png" />

1. Start the setup tutorial from the web control panel for any existing Device (or make a new one)
2. On Step 1 -  download a **.mobileconfig** DNS profile (pictured above) using Safari browser
3. Open the **Settings** app, and tap on the newly added option:  **Profile downloaded** 
4. Tap on **Install**

That's it, you're done.

> 🚧 Captive Portals
>
> If you use a lot of public Wi-Fi hotspots which have captive portals, you may find that DNS is broken on such networks, and you can't even access the captive portal itself.\
> If this is the case, select **Advanced Settings** in the above menu, and toggle on the "Bypass common domains" option. This will exclude common captive portals from using Control D. You can also add your own domains and WiFI networks using the same menu.

## Advanced Settings

You can further customize the DNS profile by clicking on the **Advanced Settings** button. 

<Image align="center" width="50% " src="https://files.readme.io/c6c07af98a51d10e969b438b5d5cd99872534dc26663a96b271bc2bbab93705f-ios_advanced_settings.png" />

You can adjust the following:

* **Client ID** - Enter any name that you want, which will allow you to see Analytics for individual physical gadgets that all use the same Control D Device. This is part of the [Device Clients](doc:device-clients) feature. 
* **Exclude Wi-FI Networks** - Here you can list Wi-Fi SSIDs where you don't want to use Control D. Handy for work networks that may block it, or your home where you already have Control D on your router. 
* **Exclude Domains** - Here you can enter specific domain names that you wish to be excluded from Control D. These will resolve using your regular ISP assigned DNS resolver. This is handy for accessing private domains or captive WiFI portals. 
  * Choose Folder - You can keep a list of domains to exclude in a folder. Choose the folder and it will auto-populate the list of domains you wish to exclude, so you don't have to type them out every time. 
* **Exclude Common domains** - This toggle will exclude common captive portals (such as on planes) to solve the [captive portal issue](/docs/doesnt-work-on-captive-portals).
* **Prevent Disablement (Org Accounts Only)** - If you're using managed (supervised mode) devices, you can toggle this option on, which will prevent the end user from disabling this DNS profile. 
* **Trust Control D Root CA** - Will bake in a Root CA certificate which can be used to display [Custom Block Pages](doc:blocked-query-response).
