---
title: N-able RMM Tutorial
excerpt: >-
  If you use N-able RMM, this tutorial will help you onboard your users to
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

In the N-able interface, go to **Settings** -> **Script Manager** and click on **New**.  

1. Name: Call this something
2. Type:  Select "Automated Task"
3. OS: check the appropriate OS boxes (using Windows as an example) 
4. Upload the script you downloaded above

![](https://files.readme.io/0617b40-image.png)

## Create Automated Task

Now select your devices, choose **Task**-> **Add**.  

![](https://files.readme.io/e024251-image.png)

1. Select the task you created above and press Next
2. Give this a name and press Next
3. Select Frequency Method: **Manual** and press Next and Finish.

![](https://files.readme.io/9388a4c-image.png)

> 🚧 Run Once
>
> Make sure to select **Manual**, and only run this task once per machine. Each execution run will create a new Device in the Control D web interface. This won't break anything, but you will see duplicate devices.

## Run Automated Task

Select your devices, and choose **Task** -> **Run**. 

![](https://files.readme.io/2448159-image.png)

Press Next and then select **Run Task**. 

![](https://files.readme.io/789dfd0-image.png)

Once the script is deployed and executed (this can take some time), you should see something like this.

![](https://files.readme.io/321ecd2-image.png)

Now if you go to Control D web panel, you should see your Devices popup in the Users section.

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
