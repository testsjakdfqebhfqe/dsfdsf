---
title: DNS64
excerpt: Support for IPv6-only networks
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is DNS64

DNS64 is a feature that allows IPv6-only networks to access IPv4 networks. DNS64 synthesizes AAAA records from A records, enabling an IPv6-only network to understand and connect to IPv4 addresses through an NAT64 gateway.

Default "well known" prefix is used: `64:ff9b::/96`

> 🚧 Don't turn this on unless you need it
>
> This feature is for IPv6-only networks. If you're on a dual-stack network (have both IPv4 and IPv6) do not enable this feature, or you will have a bad time.

## How to Use it

Edit a Profile and navigate to Profile Options. Locate the **Enable DNS64** toggle and switch it on to enable the feature. This will allow devices on the network using IPv6 to seamlessly access IPv4 services.
