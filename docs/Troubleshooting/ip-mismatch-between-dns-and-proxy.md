---
title: IP mismatch between DNS and Proxy
excerpt: >-
  Redirected traffic will not work if you're using multiple IPs at the same
  time.
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

> 🚧 Do you have redirect rules?
>
> If **not**, there is no problem here. You can safely ignore this warning, as it has no impact on you.

On the [Status Page](doc:status-page) you are presented with all IPs that Control D detected on your device. If you see that your **DNS Source IP** differs from **Proxy Source IP**, this is an unusual situation, but can happen on some cellular networks. 

# The Issue

If you notice an IP mismatch, anything you redirect via a Proxy will fail to load. If you used Default Rule -> Redirect, this will effectively break your Internet. If you're not redirecting any Service, or Custom Rule then this mismatch would not cause any issues. 

## Cause

In order to access proxies that redirect your traffic, your source IP must be authorized in the global firewall. When you make DNS queries, whatever source IP those queries come from, will get authorized automatically and everything will work as expected. However if the DNS server sees one IP, but you communicate with proxies using another, we cannot authorize your "other" IP, as we never saw it until you tried to proxy something, and this request will fail as the IP is not in the global firewall. 

# Solutions

## Disable IPv6

If you're on an IPv6 network, and find that your IPv6 addresses differ, you can disable IPv6 on your network which will resolved the problem with 99% certainty. However this may not be desirable, in which case read on.

> 📘 Caveat
>
> If you're using IPv6, a mismatch is only a factor if the 2 IPs don't fall within a /64 network. Different IPs within a single /64 network would not cause any issues as we authorize a whole /64 in the global firewall.

## Manually Authorize IP

You can use the [IP Management](doc:ip-management) section to manually authorize your **Proxy Source IP**.

## Disable Redirect Rules

You can stop using the redirection features and stick to just blocking. This may not be ideal for most.
