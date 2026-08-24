---
title: Jamf MDM Tutorial
excerpt: Deploy Control D to your MacOS.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
### 1. Create your Provisioning Token

First thing you have to do is create a Provisioning code in the Control D Dashboard. Go to **Provision**, and click the **+** button. Fill out the form, and you should see an install command as well as a button to Download Install Script.

<Image alt="" src="https://files.readme.io/a8deeac7fc9123df07611bf67afe1e30366f149c33e5cbdf7cdf26e46d4061d5-brave_screenshot_controld.com_33.png" align="center" border="true" />

<br />

> 🚧 Expiry Time and Limit
>
> Be sure to select the appropriate expiry time and execution limit for the Provisioning code. When this time passes, or the limit is reached, the code will become invalid and cannot be used anymore to provision new Endpoints. Same applies if you delete this code.

***

### 2. Create a Shell Script in Jamf Pro

1. Log in to Jamf Pro
2. Navigate to Settings → Computers Management → Scripts.
3. Click New.
4. Name it something like: Control D Agent Installation.
5. In the Script field, paste the following template (replace `YOUR_PROVISIONING_TOKEN_HERE` with the provisioning token generated in the previous steps):

```shell
#!/bin/bash

# Download and install Control D agent
sh -c 'sh -c "$(curl -sSL https://api.controld.com/dl/rmm)" -s YOUR_PROVISIONING_TOKEN_HERE'
```

<Image alt="" src="https://files.readme.io/31eddb211eb3782aab56d32be8941c6be2b4da8cfc600f959bcf47fa7865bda7-brave_screenshot_controldtest.jamfcloud.com_13.png" align="center" border="true" />

6. Click Save.

***

### 3. Create a Policy to Deploy the Script

1. Go to Computers → Policies.
2. Click New.
3. Set a descriptive name: Control D Agent Deployment.
4. Under General:  
   • Set Trigger to Recurring Check-in, Enrollment Complete, or manually via Self Service.  
   • Set Execution Frequency: Once per computer (recommended).
5. Under Scripts:  
   • Click Configure.  
   • Add the Install ctrld Agent script.
6. Under Scope:  
   • Target all Macs or a Smart Group with qualifying devices.
7. (Optional) Under Maintenance or Files and Processes, enable Update Inventory to confirm installs.
8. Save the policy.

<Image alt="" src="https://files.readme.io/b3077a55d27df8f6035d2b1e5e5289e44473b27f755e22fffde10c1b18ad47f5-brave_screenshot_controldtest.jamfcloud.com_1.png" align="center" border="true" />

***

### 4. Test Deployment

Pick one Mac from your test group and run the following to force a Jamf policy check in:

```shell
sudo jamf policy -verbose
```

3. Confirm installation:

```shell
sudo ctrld status
```

You can monitor your deployment from the Jamf dashboard:

<Image alt="" src="https://files.readme.io/07a4fc0bfb7fcb01a5010cea8592cee2f50eb9f46ac5362a250ec4b645dbbf46-brave_screenshot_controldtest.jamfcloud.com_2.png" align="center" border="true" />

Your devices should appear in your Control D Web Dashboard:

<Image alt="" src="https://files.readme.io/3767e8aaa386922ac0b5170f3016b2a34ca5a1df93f71c792071b15477f3242f-brave_screenshot_controld.com_34.png" align="center" />

***

> 🚧 Prevent Deactivation
>
> Only applies to end users with administrative access.

While you can [prevent deactivation](https://docs.controld.com/docs/prevent-deactivation) by setting a PIN code - users with admin rights can disable the `ctrld` login item via the MacOS Settings App.

To prevent this - you can deploy Configuration Profile which will prevent deactivation.

***

1. Go to: **Computers → Configuration Profiles → New**
2. Choose:

   - **macOS**
   - Give the profile a name, e.g., `Managed Login Item - ctrld`
3. Under **Privacy & Security**, click **Login Items**
4. Click **Add** under “Login Items”
5. Enter the following:

<br />

| Field             | Value                  |
| ----------------- | ---------------------- |
| Team Identifier   | `GYZJYS7XUG`           |
| Bundle Identifier |                        |
| Visibility        | `Visible` _(optional)_ |
| Hide from Users   | `No`                   |

<br />

<Image alt="" src="https://files.readme.io/9bfc1aa619bb10e1a63e4304681a005e25163e9d3ad477a0287f40e01c76551d-Jamf02.png" align="center" border="true" />

This enforces a profile that

- Prevents users from disabling the background launch item in **System Settings → Login Items → Allow in the Background**
- Makes it appear as **"Managed by your organization"**
- Locks the toggle UI