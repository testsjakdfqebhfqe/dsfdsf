---
title: Prevent Deactivation
excerpt: Set a password that is required to deactivate Control D if apps are used.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
# Overview

> 🚧 No App Removal Protection
>
> This feature will prevent the end-user from deactivating Control D within the app, but if they have admin privileges, they can remove the app from their device. You should prevent this using your MDM/RMM tool.

This Endpoint/Device Setting allows you to set a numeric PIN (password) which will be required to deactivate Control D when our GUI or CLI apps are used.


<Image src="https://files.readme.io/03fc71349d83ddc80c63797229a499d79ca70d3c4736591c2bc462b24a092879-prevent-deactivation.png" align="center" width="100%" />


This is useful in school environments or anywhere else where you wish to lock down the deactivation of Control D.

A PIN can be updated (or removed) from the Web Control Panel, however the associated physical device will need to be restarted in order for this change to propagate.

## Change or Remove Pin

In order to change the PIN or remove it, simply edit the Endpoint/Device that has a PIN and update the value in the form field, or toggle the feature OFF. Be mindful, that the physical device would need to be restarted in order for the PIN change/removal to take effect.

## Uninstall with PIN

### GUI Apps

If the configured Control D endpoint/device has a deactivation PIN enabled, you will be asked for it to disable Control D. Simply type it into the box that pops up.

### CLI Apps

To uninstall a PIN locked CLI installation, simply append `--pin xxxxx`  to the `stop` or `uninstall` commands, for example:

```
C:\WINDOWS\system32>ctrld uninstall
Apr  3 15:51:23.000 ERR deactivation pin is required to stop or uninstall the service

C:\WINDOWS\system32>ctrld uninstall --pin 1234
Apr  3 15:51:32.012 NTC Service uninstalled
```

Uninstallation on MacOS and Linux would work identically.
