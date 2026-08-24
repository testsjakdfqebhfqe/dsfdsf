---
title: iCloud Private Relay
excerpt: How to use Control D with Apple iCloud Private Relay
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is Private Relay

[Private Relay](https://support.apple.com/en-ca/102602) is essentially a double hop VPN service provided by Apple that selectively routes some requests from your Apple device to proxy servers operated by Apple, which in turn forward the traffic to 3rd party proxy servers not operated  by Apple. This effectively masks your IP address from **some** of the websites you visit.

# What is Control D

Control D is a customizable DNS service, with optional [Traffic Redirection](doc:feature-traffic-redirection) capabilities. It essentially can do everything Private Relay can (albeit using a different technology), and a whole lot more, while being customizable by the end user (you!), unlike Private Relay which is "one size fits all".

## Using Private Relay with Control D

By default, Control D will block `mask.icloud.com` and `mask-h2.icloud.com` domains, which will disable Private Relay. If you wish to keep using Private Relay in parallel (not recommended), you can do one of two things:

* Make a [Custom Rule](doc:custom-rules) to bypass the above listed domains
* Make a bypass [Service Rule](doc:services) for the Apple Service

>  **NOTE** You may still see Apple NS/TXT lookups resolved normally in the Activity Log. These are DNS metadata records and are not redirected/proxied; Apple redirect/proxy behavior applies to address lookups such as A/AAAA.

## Why is it disabled?

Control D disables Private Relay for a good reason - using both services (Private Relay and Control D) at the same time is not a good idea as both services attempt to do similar things, and unexpected behavior will occur. This includes, but not limited to:

* Delayed push notifications
* Inconsistent blocking behavior - things you blocked may **randomly** resolve as you're essentially using 2 different DNS resolvers at the same time (one from Apple and another from Control D)
* Other unexpected and unknown problems

**We do not recommend re-enabling Private Relay, unless you know exactly what you're doing.**
