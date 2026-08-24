---
title: Microsoft inTune Tutorial
excerpt: >-
  If you use Microsoft inTune, this tutorial will help you onboard your users to
  Control D.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Install

## Create Provisioning Code

First thing you have to do is create a Provisioning code in the Control D web panel. Go to **Devices** -> **Provision**, and click the `+` button. Fill out the form, and you should see an install command as well as a button to **Download Install Script**. Download this script. 

![](https://files.readme.io/5fe3c4f-image.png)

> 🚧 Expiry Time and Limit
>
> Be sure to select the appropriate expiry time and execution limit for the Provisioning code. When this time passes, or the limit is reached, the code will become invalid and cannot be used anymore to provision new Devices. Same applies if you delete this code.

## Create Script

In the inTune portal, go to **Devices** -> **Scripts** and press `+ Add`. Choose **Windows 10 or Later**. 

1. Name your script and press Next
2. Upload the Powershell script you downloaded. 
3. Set the settings as below and press Next

![](https://files.readme.io/c0d36c1-image.png)

4. Choose the appropriate Users, Devices or Groups and press Next. 

![](https://files.readme.io/b8c35d1-image.png)

5. Press Add. 

You should see a message: **PowerShell script successfully assigned**

At this point you're done. Next time the devices perform a Sync, they should download and execute the install script. This process can take anywhere from minutes, to days, depending on how lucky you are. 

Once the script is deployed and executed, if you go to Control D web panel, you should see your Devices popup in the Users section. 

![](https://files.readme.io/27bc60b-image.png)

# Upgrade

To upgrade an existing installation to a new version of `ctrld` create a Powershell script with the following contents:

```Text Powershell
(Invoke-WebRequest -Uri 'https://api.controld.com/dl/rmm' -UseBasicParsing).Content | Set-Content "$env:TEMP\ctrld_install.ps1"; Invoke-Expression "& '$env:TEMP\ctrld_install.ps1'"
```

Then execute it on target machines.

# Uninstall

If you wish to uninstall the `ctrld` client, create a new (batch or Powershell) script with the following contents:

```Text batch
ctrld uninstall
```

Then execute it on target machines.
