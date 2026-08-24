---
title: Sub Organizations
excerpt: >-
  Create Sub-Organizations in order to compartmentalize your Profiles and
  Endpoints into logical groups.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What are Sub-Organizations?

Sub-Organizations are simply groups of Profiles and Endpoints that belong together. Sub-Organizations can be any of the following:

* Departments
* Physical sites 
* Customer companies (if you're an MSP)
* Anything else you wish

All Organizations have the ability to create as many Sub-Organizations as needed.

# Create Sub-Organization

To create a Sub-Organization, expand your primary Organization, select **Sub-Organizations** and click the big `+` button. You will be presented with the following form. 

![](https://files.readme.io/9091b7937be0fc2fd3173849cc1777d995437043805f0e4f9b825ffd925eb929-image.png)

* **Name** - Name of the Sub-Organization
* **Contact Name and Email** - Who is responsible for this Sub-Organization
* **Address** - Optional physical address if any
* **Website** - Optional website if any
* **Mandatory Two-Factor Authentication** - If enabled, all members are forced to enable 2FA
* **Data Storage Region** - Where Analytics data is hosted
* **[Global Profile](doc:global-profile)** - Choose any parent Organization's Profile to enforce on all Sub-Organization's Endpoints.

Click the **Create** button and you're done. 

# Manage Organizations

Once you have more than zero Sub-Organizations, you will see them in a table. 

![](https://files.readme.io/7bc1fd3969421827c1b966a66c7577c45d8b940b507c4d94ebe9d193dea31760-image.png)

From this section, you can do the following:

* View your Sub-Organizations and how many Endpoints, Connected Devices, Profiles and Members exist in each one
* See the associated cost of the Endpoints in the Sub-Organization
* From the drop down menu, you can edit Sub-Organization details, membership and delete the Sub-Organization  
* You can impersonate an administrator of a Sub-Organization by clicking anywhere on the Sub-Organization item

### Sub-Organization Membership

By default, a Sub-Organization has no direct members (admins). Only members of the primary Organization have access to it, with the same permission level as in the primary Organization. Simply click anywhere in the row in order to view the Sub-Organization as if you're a member of it - this is called 'impersonation'. This allows for creation of Profiles and Endpoints within the Sub-Organization. 

![](https://files.readme.io/483664939d898645cc2c2f810f82094cc0917b2cf1d20388d955d8f2b3e30bb4-image.png)

If you wish to delegate access to a single Sub-Organization, you can select the **Add/Edit Members** option from the above drop down menu and invite folks directly into the Sub-Organization. The [permission scheme](doc:org-members-permissions) is the same as for the primary Organization, except invited emails would have access solely to the invited Sub-Organization. 

![](https://files.readme.io/0b3f9fc20607a4cbcce4c3065fe76c49e03b2975d0fd8ed5dbfcf87650f0536c-image.png)
