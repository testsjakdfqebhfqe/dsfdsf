---
title: Microsoft NCSI / Connectivity Warning
excerpt: >-
  Windows will sometimes claim that there is no Internet connectivity. Do not
  believe its lies.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# "No Internet Access"

If you're in an Active Directory environment and installed the [Command Line Daemon](doc:ctrld) manually or using the [Org: Mass Provisioning](doc:provisioning) flows, and you're unlucky, you see Windows claim that there is no Internet access after you reboot the machine, despite there being Internet access. Thanks Microsoft! 

<Image align="center" src="https://files.readme.io/c3702c7-windows_lies.png" />

# Solutions

## Delegate to Domain Controller

Use the [Split Horizon DNS](/docs/active-directory-integration-guide#2-split-horizon-dns) method you used for making your local domains work, and add the following rules to the **Control D Bypass** folder:

* `*.msftncsi.com` -> BYPASS
* `*.msftconnecttest.com` -> BYPASS

Then reboot the machine and your issue is *likely* to be resolved. If not, use the 2nd method. 

## Global DNS

Open **admin cmd** and execute the following command:

```Text cmd
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\POLICIES\MICROSOFT\Windows\NetworkConnectivityStatusIndicator" /v UseGlobalDNS /t REG_DWORD /d 1 /f
```

This command configures Windows to use global DNS servers for its internet connectivity checks, which should help avoid the issue, if you encounter it. After running the command reboot the machine to validate the fix.

### Group Policy

Alternatively, you can do this using Group Policy. Head over to `Computer Configuration > Administrative Templates > Network > Network Connectivity Status Indicator`, enable the "Specify Global DNS" option and run `gpupdate /force`. Then reboot the target machine.
