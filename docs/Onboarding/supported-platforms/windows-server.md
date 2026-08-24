---
title: Windows Server / AD Controller
excerpt: How to setup Control D on a Windows server / AD domain controller
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: active-directory-integration-guide
      title: Active Directory Integration Guide
---
# Overview

>  "I sure can't wait to make changes to my domain controller" - nobody, ever.

Managing Windows servers can be challenging, so let's make this as simple as possible. There are two ways to deploy Control D on your Windows DNS Server / AD domain controller. 

## Legacy DNS

This method requires no software to install, and is quite easy. Simply create a Windows Server [Device](doc:devices), and be sure to toggle the [Legacy Resolver](doc:legacy-resolver) option. Once you have your DNS resolver IP addresses, simply set them as  forwarders in the DNS Manager. 

<Image alt="The above IPs are just for example, yours will be different." align="center" src="https://files.readme.io/4743876-Untitled.png">
  The above IPs are just for example, yours will be different.
</Image>

That's pretty much it. As long as the source IP of your network is [known to Control D](doc:ip-not-authorized), everything should just work now. 

Keep in mind, you're still use Legacy DNS, which is not encrypted and you also miss out on some [unique features](doc:device-clients) of Control D. If you want to leverage modern DNS protocols and features, see the next method.  

## Secure DNS

This method requires the installation of our [Command Line Daemon](doc:ctrld). This is not as scary as it sounds, and is quite literally a single command. Simply create a Windows Server [Device](doc:devices), and click on Automatic Setup button.

> 🚧 Windows Server 2019+
>
> You must have at least the 2019 version of Windows Server installed. 2016 and earlier are not supported.

You will see multiple methods of installation, the one you want is the batch command.

![](https://files.readme.io/30fbd66-image.png)

Copy this command and paste it into **cmd**. You will see something like this. 

<Image align="center" src="https://files.readme.io/71038b8-Untitled2.png" />

Here is what happened:

* A script is downloaded and executed
* Script detects the correct arch and downloads the `ctrld.exe` binary into `C:/ControlD` directory
* `ctrld.exe` is added to system path, so you can call it from any (new) terminal. 
* System service is added and started, which spawns a localhost DNS listener
* ctrld configures the listener as a forwarder in Windows DNS

<Image align="center" src="https://files.readme.io/acdec75-Untitled3.png" />

You're (almost) done here. See [Active Directory Integration Guide](doc:active-directory-integration-guide) for more relevant material if you want your local domains to still exist (it will be painless, we promise).
