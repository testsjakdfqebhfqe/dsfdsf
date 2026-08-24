---
title: Routers
excerpt: How to configure Control D on most routers.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Control D can be configured on most routers with variable degrees of ease, depending on what DNS protocols your router supports, and whether you have a Static IP or not. 

# Secure DNS

If your router natively supports DNS-over-HTTPS or DNS-over-TLS, this is the easiest (and best) option. Simply input your Device's DNS resolvers into the router interface and you're done. This is the best and preferred method of using Control D, as it's not subject to any of the [Legacy DNS limitations](doc:ip-not-authorized). 

Unfortunately, most routers do NOT support Secure DNS natively, in which case you have to use the other methods documented below. 

# Legacy DNS

Most routers do not support Secure DNS protocols, so you're going to have to use Legacy DNS IP addresses associated with the Device you've created in the web panel (be sure to enable the [Legacy Resolver](doc:legacy-resolver) Device setting).

> 🚧 Dynamic IP Warning
>
> This method is subject to your [source IP being registered](doc:ip-management) on this Device in the web control panel, so this is best suited for networks with a static IP. If you have a Dynamic IP see [Legacy DNS limitations](doc:ip-not-authorized) section for solution.

# DNS Proxy Daemon (ctrld)

If your router is on a dynamic IP address, or if you wish to use Secure DNS protocols anyway (you really should), you can use the open source [Command Line Daemon](doc:ctrld) in order to do this.

## Supported Routers

The `ctrld` daemon currently supports 1 liner installation command on the following routers / firmware:

* ASUS Merlin
* OpenWRT
* DD-WRT
* Fresh Tomato
* Firewalla
* Ubiquiti UDM, UDR, EdgeRouter
* GL.iNet
* Synology
* pfSense / OPNsense

Other routers may be supported, but you have to do some some manual work, which involves:

* Making sure `ctrld` launches on boot / runs as a system service
* Steering DNS traffic to the listener

## Automatic Install

To do this in the quickest possible way click **Add Endpoint** and go to **Devices -> Routers** section. Choose your router vendor or firmware.  

<Image align="center" width="50% " src="https://files.readme.io/ccc68d6b724ae43074fa6ef76e581ec7d48ed1df19bbcd66bb1f96879cd84449-Add_Router.png" />

Give it a name and set appropriate settings. 

<Image align="center" width="50% " src="https://files.readme.io/ca544b0c2f0d78cd84c3838829e7d4485c65b59ae0676818760ffcf03e62a9f9-Name_Router.png" />

Once you add this Device, you will be presented with a Resolvers screen. If you know what to do with these - go do that. Otherwise read on. 

<Image align="center" width="50% " src="https://files.readme.io/c1c69d8824075c4ce5b6c73639b127c5d13d19558db99ba6a3922fd0c9752d0c-Router_Resolver_ID.png" />

From here, you can click **Help Me Configure > Automatic Setup** button which will kick off an incredibly uncomplicated 1-step setup process. Simply copy the command, and paste it into your router's SSH shell. 

<Image align="center" width="50% " src="https://files.readme.io/ecfe10715109c94eb0bed30380f9a4bdee5d6832023437fcd9b814789cf3dd76-Router_1-liner.png" />

As soon as you do, you should see a checkmark in the bottom right corner. That means you're done. 

## Manual Install

Simply download and run the binary that is appropriate for your router architecture, and follow the instructions in the [README on Github](https://github.com/Control-D-Inc/ctrld#readme). Alternatively, you can use a [1 liner command](/docs/ctrld#quick-install) to install `ctrld` automatically.
