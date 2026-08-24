---
title: Atera RMM Tutorial
excerpt: How to setup Control D using Atera RMM
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

First thing you have to do is create a Provisioning code in the Control D Dashboard. Go to **Provision**, and click the **+** button. Fill out the form, and you should see an install command as well as a button to Download Install Script.

<Image align="center" className="border" border={true} src="https://files.readme.io/fb5f9ece4824b30be93b9efe2fda5d750ea3a553486d6b70359777e877082e6a-brave_screenshot_controld.com_10.png" />

> 🚧 Expiry Time and Limit
>
> Be sure to select the appropriate expiry time and execution limit for the Provisioning code. When this time passes, or the limit is reached, the code will become invalid and cannot be used anymore to provision new Endpoints. Same applies if you delete this code.

***

<br />

## Create a Deployment Script

* From the Atera UI navigate to `New` in the top left corner and choose `Script`.

<Image align="center" className="border" border={true} src="https://files.readme.io/1891d8f97d60cc57c4b6dfa4b9877b81819f243b3c0d4650f2c62003c4f76e36-AteraNewScript.png" />

* Fill out the required fields as you see fit.

> 🚧 Permissions
>
> Be sure you've selected **System** for the `Run As` option.

* Paste the Provisioning Script you created in the previous step *OR* upload the script you downloaded.

* Save & Exit.

<Image align="center" className="border" border={true} src="https://files.readme.io/32c00418ce15080563bc2f8a2a6f7cf2c8027482f8219c1f58524aabc0baedf9-AteraInstall.png" />

### Create Upgrade Script (Optional)

* Create a new PowerShell script with the following:

```powershell PowerShell
ctrld upgrade
```

### Create Removal Script (Optional)

* Create a new PowerShell script with the following:

```powershell
ctrld uninstall -vv
```

<br />

***

<br />

## Deploying to Windows Endpoints

* From the `Devices` tab - select the endpoints you plan on deploying to and choose `Run Script`.
* Choose your Installation Script and adjust your Script Execution Preferences.
* Run the script.

<Image align="center" className="border" border={true} src="https://files.readme.io/650db7ce0d5375f053b0bfee3d6a95398e5d690c93bbceeb4dc3b69211b8301e-AteraDeploy.png" />

* View the progress of your deployment by navigating to `Reports --> Classic Reports --> Recent Processes` or by viewing an individual endpoint page.

<Image align="center" className="border" border={true} src="https://files.readme.io/6fa8da382c0d39008de0ab80a5ca8665281824dcdee52b6b1211144e8c2a6ac1-AteraInstall03.png" />

Once your deployment is finished - you should see your Endpoints in the Control D Dashboard.

<Image align="center" className="border" border={true} src="https://files.readme.io/6666f986bac937cdd9293864034d4c6aa09deb1a4746ed1d838ff9eaddd2d7f1-ControlDEP.png" />

<br />

***

## Deploying to MacOS and Linux Endpoints

MacOS and Linux follow a similar setup method, instead deploying a shell script in place of PowerShell.

* After creating a provisioning code - copy the 1-liner provisioning command or download the script.
* From the Atera Dashboard - Create a new script.
* Paste the 1-liner provisioning script or upload the full script you downloaded.

<Image align="center" className="border" border={true} src="https://files.readme.io/cce97a21d12d943cd375cd52fec9c5432f7c387be917ef5c8c08b30f93612962-Screenshot_2024-08-29_at_15-40-45_Atera_-_RMM_software_PSA__Remote_Access_for_MSPs.png" />

<br />

### Create Upgrade Script (Optional)

* Create a new shell script with the following:

```Text shell
ctrld upgrade
```

### Create Removal Script (Optional)

* Create a new PowerShell script with the following:

```shell shell
ctrld uninstall -vv
```
