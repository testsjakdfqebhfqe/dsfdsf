---
title: Device Clients
excerpt: >-
  Using Control D on a router or other types of devices, and want granular
  visibility and control? This should get you started.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

You are using Control D on a router, which likely has many devices using it as the DNS server. By default, all of these physical devices will be grouped together, and you will see the sum of all their activity, without knowing which gadget is responsible for what. Additionally, all of these gadgets will be subject to the same set of rules, defined in the enforced Profile. 

The solution to both of these issues is simple, and there are two ways to go about it. 

# Router Utility

The simplest (and best) option is to install the [Command Line Daemon](doc:ctrld) on your router. Once you do this, `ctrld` will relay LAN client information along with the DNS queries themselves, and you will see all your LAN clients in the web control panel. You can see a count of all detected clients right in the Endpoints section

![](https://files.readme.io/c4d36a6a5b5fbf85904d20c7afea5ed409e23f4914cdbe6225b1185fa9afd2e9-image.png)

If you click the "Clients" button you will see a list of all detected LAN clients. 

![](https://files.readme.io/b3df9d36a1ad0c7e9de1140de6bc90f2cd7ebdbb244ee2c2f3d6f9d55ff0fc15-image.png)

From here, you can view Analytics for chosen LAN clients, and assign them aliases. All relevant client information will be displayed here, which includes:

* **Hostname** which is the device name
* **Time** of last activity 
* **MAC address** of the device as seen by your router
* **LAN IP** address of the device assigned by your router

> 🚧 DNS-over-HTTPS Only
>
> You must be using the DNS-over-HTTPS protocol in order to see the client data. If you're using DNS-over-TLS or DNS-over-QUIC, no client data will be relayed with the DNS queries.

## Client Specific Profile

At this point you can see all your LAN clients, and view their individual Analytics, however they are all still subject to the same set of rules, as defined by the enforced Profile of the relevant Endpoint. To make one (or more) of the clients enforce a different set of rules (Profile) you can click on the Profile name in this list, and choose a different one to enforce from the drop down menu.

![](https://files.readme.io/d7796726acbc7c1756cdc10854e61b9c2612fca2d72ff4e42abb0dcedf17fd94-image.png)

Once you press Save, this Client will be subject to a different set of rules, as per the chosen Profile. 

![](https://files.readme.io/79a59833e26af3822931fcd117af1b291987ef5fd22dee4265e4c6197d35f5da-image.png)

<br />

> 🚧 Analytics Reset
>
> When you turn a LAN client into its own standalone Device, this will create a new Analytics time series. Existing data will still be available in the same place as before, however all new activity will be logged under the newly created Device, **if you enabled Analytics at device creation time**. You don't have to enable Analytics, if you want one of your LAN clients to stay hidden :)

# Using Apps

Control D has [GUI Based Apps](doc:gui-setup-utility) for Windows, Mac, iOS and Android. Simply download the relevant one for your platform. Input the Resolver ID into the box for the relevant Control D Device you want to setup, and optionally enter the client name. Then you will be able to view Analytics for all the individual clients separately. 

![](https://files.readme.io/f44ebd1-image.png)

# Manual

If you're not using the `ctrld` utility, you can still make use of the above system, albeit with some limitations, and you won't see all of the data mentioned above (hostname, MAC address, LAN IP). 

To manually "create" a client for a [Device](doc:devices) simply template the DNS-over-HTTPS URL or DNS-over-TLS  hostname with the client name, and configure the resolvers on desired physical gadgets. After you do, you will be able to view Analytics separately for all the clients. For example:

### DNS-over-HTTPS

* Original Device Resolver: `https://dns.controld.com/abcd1234`
* Client Specific Resolver: `https://dns.controld.com/abcd1234/name-goes-here`

`name-goes-here` must not contain spaces or any special characters. Only letters, numbers and dashes are allowed. 

### DNS-over-TLS

* Original Device Resolver: `abcd1234.dns.controld.com`
* Client Specific Resolver: `abcd1234-name-goes-here.dns.controld.com`

`name-goes-here` must not contain spaces or any special characters. Only letters, numbers and dashes are allowed.

### Apple / DNS Profile

If you're using an Apple device, you can leverage DNS Profiles to achieve this. Simply create a single MacOS or iOS Device for all your Apple gadgets. Then start the setup tutorial by pressing **Help Configure.** Choose **Manual Setup**. In the **Advanced Settings** section, input the client name into the top box. 

![](https://files.readme.io/89c0b41-client_id.PNG)

Download the DNS Profile and continue with the setup flow. 

### Android Private DNS

When setting up your Android device manually using Private DNS, simply follow the DNS-over-TLS flow mentioned above. 

# Use Case

You can use this method if you want to prevent "device sprawl" where you're making a separate device for every physical gadget that belongs to a single person, ie. your kid's devices (Johnny's phone, iPad, PC).  You can just make a single Device - "johnny" and deploy a modified resolver on each of the devices. Then you can see Analytics for all their devices as a sum, or look at individual stats. You can also re-map an existing client to its own standalone Device, which enforces a unique Profile.
