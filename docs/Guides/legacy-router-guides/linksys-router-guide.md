---
title: Linksys Router Guide
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
# Legacy DNS

Here are the steps to set up Control D on your Linksys router. 

Keep in mind that Linksys routers use legacy DNS at the moment.

## Step 1

Open the router interface by navigating to it in your browser. In most cases you can reach it via `linksyssmartwifi.com` or `192.168.1.1` 

![](https://files.readme.io/7d1d9de-image.png)

![](https://files.readme.io/b05457d-image.png)

## Step 2

Log into your router with the admin password.

![](https://files.readme.io/d662b1d-image.png)

If you are prompted to log in with email, choose the Local Access option at the bottom and you will get the router password option:

![](https://files.readme.io/86abefa-image.png)

## Step 3

Click **Connectivity** in the Router Settings sidebar.

![](https://files.readme.io/23bea26-image.png)

## Step 4

Select the **Local Network** tab.

![](https://files.readme.io/5ba5e51-image.png)

## Step 5

Now determine which DNS resolver you want to use. 

### Free Resolver

If you are configuring our free DNS resolvers, you can get the IPs from this page: [https://controld.com/free-dns](https://controld.com/free-dns) 

1. Select the configuration you want to use from the list:\
   ![](https://files.readme.io/f86c0c1-image.png)

2. Then copy the Legacy Resolver IP address that appears at the bottom of the page:\
   ![](https://files.readme.io/c1b2ca6-image.png)

### Custom Resolver

If you are configuring a custom Legacy DNS resolver: 

1. Create a new "Other" Router Device on your [Control D Dashboard](https://controld.com/dashboard/devices). Link it to a Profile (or [create a new Profile if you don't have one](https://docs.controld.com/docs/profiles)) and finally make sure to enable the **Legacy Resolver** option under **Advanced Settings**. Then press **Add Device**:\
   ![](https://files.readme.io/708cf50-image.png)

2. Expand the **Legacy DNS** section where you will see the IP addresses to use for the setup. Do NOT copy the same IPs from the screenshot, copy the ones from your account specifically.\
   ![](https://files.readme.io/6796a58-image.png)

## Step 6

The **DHCP Server** section on the right will contain the **Static DNS** fields you need. We will use the two resolver IPs you chose in the last step.

Enter those IPs in the **Static DNS 1** and **Static DNS 2** fields. If the fields are greyed out, make sure the **DHCP Server** option at the top is **Enabled**.

![](https://files.readme.io/a427c10-image.png)

## Step 7

Finally, scroll to the bottom of the page and press **Apply**. 

![](https://files.readme.io/87d53ca-image.png)

Press OK to confirm.

![](https://files.readme.io/1f5f5e1-image.png)

Once the router saves the configuration, you are using Control D on your network! 

Keep in mind that if you configure a custom DNS on any of the individual devices connected to this router, those devices will not be using the DNS you configured here.

> 🚧 Dynamic IP Warning
>
> This method is subject to your [source IP being registered](doc:ip-management) on this Device in the web control panel, so this is best suited for networks with a static IP. If you have a Dynamic IP see [Legacy DNS limitations](doc:ip-not-authorized) section for solution.
