---
title: TTL Overrides
excerpt: Override default DNS record TTLs with your own.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is DNS TTL

Every DNS record has a TTL, which instructs the OS to cache the DNS record for that period of time (in seconds) and not contact the DNS server for at least that long. This is used to reduce the amount of DNS queries clients make, and can have positive performance implications. 

This Profile Option allows you to override the TTLs to whatever values you wish. This feature can sometimes be called "Cache Boost", if you increase the TTLs to non-default values. By doing so, you instruct your OS to cache DNS records for longer periods of time. 

**NOTE** that if you toggle these on but *do not* change the default values presented at first, no change will be implemented (the first number you see will be what it's already set to).

> 🚧 Know what you're doing
>
> Don't change these randomly, or set them too high as this can have adverse consequences with CDNs. By high we mean "measured in days".

There are 3 TTLs that you can tweak in Profile Options. 

<Image align="center" src="https://files.readme.io/0dd2a302d6b46fae702d5957ef802f476590fba49c44cb2cfba5879f71298146-TTL.png" />

## Block TTL

This overrides the TTL for DNS records that were blocked by Control D. The **default block TTL is 10s.** Increasing this value will result in fewer DNS lookups (for things that are blocked), but will also increase the time between you unblocking the domain and it actually becoming unblocked. 

## Redirect TTL

This overrides the default TTLs on DNS responses that were redirected by a Service, Custom Rule or Default Rule. The **default redirect TTL is 20s**. Increasing this value will result in fewer DNS lookups, but will also increase the time between you changing locations and your new location settings being actually enforced on a Device.

## Bypass TTL

This overrides the TTL for all DNS records that were bypassed (not subject to any BLOCK or REDIRECT rule) and sent to the upstream resolver. Increasing this value will result in fewer DNS lookups, but can break websites if you set this too high. Values above 1 day are not recommended.
