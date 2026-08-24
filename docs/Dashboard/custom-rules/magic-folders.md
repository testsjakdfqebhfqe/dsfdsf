---
title: Magic Folders
excerpt: Some folders are special and can unlock advanced behaviors.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What are Magic Folders

There are special folders that you can create that allow you to enforce advanced behaviors.

## Control D Bypass

<Image border={false} src="https://files.readme.io/1cba0e7316f523d2f337e108ba01dbd4c2edc4f13d29ad5ec493025c0056853f-image.png" />

This Magic Folder allows you to split route DNS queries from ever reaching the Control D. Instead, these would be handled by the default DNS server on your network (domain controller, captive portal, etc). In order to do this, create a folder with this exact name in a Profile enforced by your roaming devices: `Control D Bypass`.

Any **enabled** BYPASS rule that you put into this folder will get excluded from using your Control D DNS resolver. Rules can be exact hostnames (`wifi.airline.com`), or wildcards (`*.airline.com`).

### Why Use This

This is handy in several scenarios, which include but are not limited to:

* Split routing local domains and delegating resolution to an [AD domain controller](/docs/active-directory-integration-guide) (or any other local DNS server)
* Bypassing captive portals

> 📘 Common Captive Portals
>
> We're already excluding common captive portals for major airlines and those that were reported to us by users. There is a good chance you don't need to worry about this. However if you encounter a captive portal that indeed does not work, then read on!
>
> **NEW: If you're using`ctrld` v1.3.10 or newer, you no longer have to manually bypass captive portals, as this happens automatically (in most cases).**

These rules are not instantly applied, since a configuration has to be re-fetched from Control D in order to be enforced locally on the relevant physical devices.

### GUI app or ctrld daemon

> 🚧 FYI
>
> This works only if you're using `ctrld` in default mode, using the 1 liner installer. If you're using a custom config, you have to edit it manually.

If you use our apps (GUI or CLI), in order for newly added bypass rules to be enforced, local settings must be reloaded. This can be done one of 3 ways:

* **Visit the [Status](https://controld.com/status) page** - changes will be instantly applied
* **Wait up to 1 hour** - changes are re-fetched from API every hour automatically
* **Run command** - fetch + reload the `ctrld` config file using the `ctrld reload` command

### Apple DNS Profile

These cannot be updated, as rules are baked in into the DNS profile (.mobileconfig) itself. You will have to re-download and re-install the DNS profile. Sorry about that.

## Do Not Log

<Image border={false} src="https://files.readme.io/1fb1ed7953ed2ccb2e02353a4a5953fb33701c0f1368ec94cdbdb98744badb76-image.png" />

This magic folder allows you to exclude domains from being logged into Analytics. Create a folder with this exact name in a Profile enforced by relevant Endpoints: `Do Not Log`. Any custom rule you put into this folder will be acted upon, but will not be logged into Analytics.

### Why Use This

This is handy if you see a "spammy" domain polluting your Analytics, or want to mask the activity for that one special domain that you access a lot.
