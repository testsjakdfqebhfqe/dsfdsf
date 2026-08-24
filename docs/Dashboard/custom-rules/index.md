---
title: Custom Rules
excerpt: Fine grained control over individual domain names.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 📘 TLDR
>
> Custom Rules are basically a hosts file, with wildcard support. Block, redirect or spoof any domain to any IP.

# What are Custom Rules

Custom Rules are the basic building blocks of Control D, and allow you to create fine grained rules for specific domain names. Think of these as a hosts file in the cloud, with wildcard support. 

You can have up to 10,000 Custom Rules.

To create a custom rule, choose a Profile and click Edit. Then navigate to the Custom Rules section.

<Image align="center" src="https://files.readme.io/b0ea67eef7375b595dc8a569265802fec16dab0c856b61a74f9dfeeb9acede6b-Screenshot_2025-08-20_at_11.46.02_AM.png" />

## Rule Actions

Much like with Services (which are just collections of Custom Rules), one of 3 rule types can be attached to any domain name.

### Block

A BLOCK action will prevent the domain from loading, and will effectively make it inaccessible from a Device that enforces a Profile.  

### Bypass

A BYPASS rule will resolve the domain to its true IP address from Authoritative DNS. This is useful to override Filters, Services, or the Default Rule. 

### Redirect

A REDIRECT rule will spoof the domain via a proxy location or specific IP address chosen by you.

Custom Rules can be grouped into Folders, which can have their own actions.

## Create Private Domains

If you wish to create a private domain, when you make a Custom Rule, choose Redirect and then select **IP or Hostname** instead of **Proxies**.

This is very useful for those who are using Active Directory and need to make their domain controllers still function while Control D is used as the primary DNS resolver. 

<Image align="center" src="https://files.readme.io/90f6f7c0146ee1422c2da71440a7ab5e3cd04d97659723dec4bbc962ef8613df-Screenshot_2025-08-20_at_11.49.47_AM.png" />

This will allow you to input your own IPv4 and IPv6 (or CNAME) records. Any Device that enforces this Profile will be able to resolve these custom domains, which do not exist in public DNS. 

If you're in an AD environment, simply replicate the domain controller hostnames and the IPs they point to. Any device that enforces this profile will now be able to resolve your domain controllers. 

## Overlapping Rules

Control D will match the most specific rule first. With that in mind, you can create overlapping rules, for example:

<Image align="center" src="https://files.readme.io/71780d91c4a5195de6279bd43cd7764e8550641e2d7becf0de8a3b577dfad1cc-Screenshot_2025-08-20_at_11.48.09_AM.png" />

The above will block `live.com` and all subdomains on `live.com`. However if a user accesses `outlook.live.com` specifically, this will be allowed to resolve. 

# Rule Format

Custom rules can be exact or use wildcards. All of the following are valid:

| Domain and Rule                | Action                                                                    |
| :----------------------------- | :------------------------------------------------------------------------ |
| `domain.com` -> BLOCK          | Blocks domain.com and all subdomains                                      |
| `*.domain.com` -> BLOCK        | Blocks all subdomains of domain.com but NOT domain.com                    |
| `server-*.domain.com` -> BLOCK | Blocks  `server-01.domain.com` and `server-anything-goes-here.domain.com` |
