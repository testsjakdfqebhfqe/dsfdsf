---
title: Self-Provisioning
excerpt: Control D can be setup by the end user quickly and easily.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Have dozens of hundreds of end-users and wish to deploy Control D on all their individual devices? We can already sense how NOT excited you are about doing this. Don't be sad, this is going to be surprisingly painless.  

> 🚧 Admin Rights Required
>
> To use this onboarding method, the end user must have admin rights on their machine. If they do not, please see [Org: Mass Provisioning](doc:provisioning) flow.

# Create Endpoint

When you create an Endpoint, a unique set of DNS resolvers is issued for that Endpoint. If you are the end-user, you can simply click "Help me configure this" button, which will kick off a setup tutorial for the chosen platform. 

![](https://files.readme.io/ddb8f2e-image.png)

# Get Link

If you are NOT the end user of the Endpoint you just created, or simply want to set it up on an Endpoint that isn't logged in into the web control panel, click the **Copy setup link** button and send it to the end user (or yourself) via any method you want. 

# Self-Setup

The end user clicks the link and follows the same setup process you would if you clicked the  "Help me configure this" button, using step by step tutorials .They do not have to be logged in (or be a Control D user) to use the self-provisioning link. 

![](https://files.readme.io/db95df5-self-configure-link.JPG "self-configure-link.JPG")

![](https://files.readme.io/d87280b-image.png)

![](https://files.readme.io/ceccd13-small-install_type.PNG)

## Confirm End User Setup

When you view a list of your Endpoints, you will see them in one of two states: 

* **Pending** - A big purple button will be shown
* **Active** - No purple button will be shown

![](https://files.readme.io/1889ff6-configured-vsunconfigured.JPG "configured-vsunconfigured.JPG")

Once a Endpoint flips from pending to active, that means the end user successfully configured the Endpoint. The little gray orb next the the Endpoint icon will turn green when the Endpoint is currently active (resolved something in the last 5 minutes) - **only if you enable Analytics on the Endpoint**. 

# Mass Create Endpoints

> 📘 Organizations Only
>
> An Organization account is required to use this feature.

Too tedious to create hundreds of Endpoints manually? No problem, simply use the [Org: Add Multiple Endpoints](doc:add-multiple-devices) flow.  Once you do this, the following will happen:

1. For each email, a Endpoint will be created with the username as the Endpoint name (ie. [bob.smith@company.com](mailto:bob.smith@company.com) -> `bob-smith` will be the Endpoint name)
2. The end user will be sent an email with a setup link for them to self-provision.

If you have total control over the end-user Endpoints (Group Policy or RMM), you can use the [Command Line Daemon](doc:ctrld) to do scripted deployments. See [Org: Mass Provisioning](doc:provisioning) for more details.
