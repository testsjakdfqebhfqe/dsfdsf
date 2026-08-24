---
title: Doesn't work on captive portals
excerpt: Using Secure DNS on Wi-Fi with a captive portal doesn't have to be difficult.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

If you're using a Secure DNS protocol like DNS-over-HTTPS or DNS-over-TLS, you may have issues on public Wi-Fi captive portals. These are the things that ask you to agree to terms, or pay before you get Internet access. 

Such networks present a chicken or the egg problem: Your DNS resolver will not be reachable until you agree to terms or pay, but you cannot load the captive portal itself to do so, since DNS is unreachable.

# Solution

The solution depends on your platform. 

## Windows

### GUI Setup Utility

Install our [GUI Setup Utility](doc:gui-setup-utility). It will bypass common captive portals and allow them to work. If you encounter one that does not work, contact support at [help@controld.com](mailto:help@controld.com) and we'll add it to the list. Be sure to check out [Magic Folders](doc:magic-folders).

### ctrld CLI Utility

Our [CLI Utility](https://github.com/Control-D-Inc/ctrld/releases) when used with the `--cd` or `--cd-org` flags will configure the device to bypass common captive portals and allow them to work.

## Mac

Here you have 3 options. 

### GUI Setup Utility

Install our [GUI Setup Utility](doc:gui-setup-utility). It will bypass common captive portals and allow them to work. Be sure to check out [Magic Folders](/docs/folder-rules#magic-folders). 

### Manual DNS Profile

When generating a [DNS profile](doc:macos-platform), select **Advanced Settings** and toggle ON the "Exclude Common Domains" option. This will bypass common captive portal domains from using Control D. You can also add your own exclusions using the revenant field. 

### ctrld CLI Utility

Our [CLI Utility](https://github.com/Control-D-Inc/ctrld/releases) when used with the `--cd` or `--cd-org` flags will configure the device to bypass common captive portals and allow them to work.

## Android

Install our [GUI Setup Utility](doc:gui-setup-utility). It will bypass common captive portals and allow them to work.

## iOS

Here you have 2 options. 

### GUI Setup Utility

Install our [GUI Setup Utility](doc:gui-setup-utility). It will bypass common captive portals and allow them to work.

### Manual DNS Profile

When generating a [DNS profile](doc:ios-platform), select Advanced Settings and toggle ON the "Exclude Common Domains" option. This will bypass common captive portal domains from using Control D.
