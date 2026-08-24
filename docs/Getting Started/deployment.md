---
title: Deployment
excerpt: How to deploy Control D on your devices.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This section provides a very brief overview of how to deploy and configure Control D. 

For more detailed explanations, please refer to the Onboarding section. 

# Create an Endpoint (resolver for your devices)

The first thing you need to do is create an [Endpoint](doc:devices) that you plan to deploy and configure Control D with. 

<Image align="center" width="200px" src="https://files.readme.io/48650168eaea02f6257a7c9d60c8e9f8e15a1f95db8caf49aae817e76fa230ec-image.png" />

From the Endpoints section of the Dashboard, click the green + button and use the handy Endpoint creation wizard. You will be presented with a unique set of DNS resolvers for that Endpoint.

* DNS-over-HTTPS
* DNS-over-TLS
* DNS-over-QUIC
* If selected in Endpoint settings, Legacy DNS (IPv4/IPv6 listeners)

At this point, if you know what to do with these, you can configure them on whatever device you desire. If you're unsure, you can click the "Help Configure" button. This will kick off a tutorial on how to do it.

# End User Self-Provisioning

If you are not the end user of this Endpoint, you can click the "Copy Setup Link" button, and send the provisioning URL to the end user. Once they click it, they will be presented with the same tutorial in order to onboard. 

Learn more about [Self-Provisioning](doc:self-provisioning).

## Software is Optional

Most modern operating systems support Secure DNS protocols like DNS-over-HTTPS and DNS-over-TLS. This means that no software is required to be installed in order to use Control D. No software means there is nothing to update, and fewer things can go wrong. The operating systems that support Secure DNS include:

* Windows 11
* MacOS Big Sur or newer
* iOS 14 or newer
* Android 9 or newer

**The above mentioned OSes do not need any roaming clients.** Read on. 

## Software is Available

Regardless of OS support (or lack of support) for modern DNS protocols, you're probably looking to deploy Control D with as few steps and issues as possible, this is why we offer two different software applications which will make onboarding a breeze. 

Learn more about [Available Software](doc:software). 

# End User Mass Provisioning

If your end users don't have admin rights to their machines, you're going to have to deploy Control D yourself, using your favorite RMM or Group Policy. Fortunately, there is a very quick way to do this. 

Learn more about [Mass Provisioning](doc:provisioning).

# Router Deployment

In order to deploy Control D on a router or locally running DNS server, you have to change the DNS upstream to one of the Control D DNS resolvers associated with a Device you created. There are 3 ways you can go about doing this.

Learn more about [Router deployments](doc:routers-platform).
