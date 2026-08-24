---
title: Legacy DNS
excerpt: Issue IPv4 and IPv6 legacy DNS resolvers to use on older physical devices.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
# What is Legacy DNS

A Legacy Resolver is a UDP 53 based DNS resolver, and it's just an IP pair. If you're deploying Control D on a device that does not support Secure DNS protocols, you have to enable this feature. Once you do, you will be issued with 2 pairs of Legacy DNS resolvers: 2x IPv4 and 2x IPv6.

## Example Devices

Here is a short list of operating systems and device types that require Legacy DNS resolvers

- Windows 10
- Most routers
- Android TV boxes
- Smart TVs

## How to Use

Simply edit an Endpoint and toggle the feature ON. Then view your resolver configuration to see your Legacy DNS IPs.


<Image src="https://files.readme.io/22388d18f97bdec3acf9f5f65f01b954eb0b6cd27443d615af1ee724cc485601-legacy-dns.png" align="center" width="100%" />


> 🚧 Limitation
>
> Legacy DNS resolvers require the source IP of the client to be known to Control D. See the next section to learn more on how that works, and how it can be automated. For troubleshooting, [see this page](/docs/ip-not-authorized).

<br />
