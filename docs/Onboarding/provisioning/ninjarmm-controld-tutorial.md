---
title: NinjaRMM Tutorial
excerpt: >-
  If you use NinjaRMM, this tutorial will help you onboard your users to Control
  D.
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

First thing you have to do is create a Provisioning code in the Control D web panel. Go to **Endpoints** and click the  **Provision** button. 

![](https://files.readme.io/c0546f6b98cb2f9ce149cf30db0606b2f7722313c61f1f043ba178fd87401529-image.png)

Then click the `+` button and fill out the form.

![](https://files.readme.io/c922e912bd467172d075ef6669adfe80bd5b342006aae44afd25ec0a34a777fc-image.png)

You should see an install command. Copy it.

![](https://files.readme.io/8bc542bd01d17104c375f6b63235a87b3ba40915c59f744e262e85c22dfe0f24-image.png)

<br />

> 🚧 Expiry Time and Limit
>
> Be sure to select the appropriate expiry time and execution limit for the Provisioning code. When this time passes, or the limit is reached, the code will become invalid and cannot be used anymore to provision new Devices. Same applies if you delete this code.

## Create Script

Now let's create an install script in NinjaRMM. Go to **Administration** -> **Library** -> **Automation**, click the Add button and choose **New Script**. 

Paste the command into the box, choose **Language = PowerShell**, fill out the rest of the fields as required, and press Save. 

![](https://files.readme.io/4c69bd4-image.png)

## Execute Script

In NinjaRMM, go to your Devices list. Choose the desired devices, select **Run** -> **Run Automation** -> **Script**. 

![](https://files.readme.io/89bb065-image.png)

Then choose the script you just created, and **Run** it as **System**. Within a few seconds, you should see this in your Activities log for the relevant device in NinjaRMM.

![](https://files.readme.io/c1f906b-image.png)

That's it! You're done. If you go to Control D web panel, you should see your Devices popup in the Users section. 

![](https://files.readme.io/27bc60b-image.png)

# Upgrade

To upgrade the `ctrld` daemon to the latest version, create a new (batch or Powershell) script with the following contents:

```Text batch
ctrld upgrade
```

Then execute it on target machines.

# Uninstall

If you wish to uninstall the `ctrld` client, create a new (batch or Powershell) script with the following contents:

```Text batch
ctrld uninstall
```

Then execute it on target machines.
