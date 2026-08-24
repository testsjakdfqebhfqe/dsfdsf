---
title: Default Rule
excerpt: When nothing matches, this will.
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
> This is the "final rule" that performs an action when no other rule matched. The default behavior is to resolve via authoritative DNS, but you can do other things too.

# What is Default Rule

As the name (hopefully) suggests, this is a special Custom Rule, that is used as a catch-all. **If a DNS query is not matched by a Filter, Service Rule, or any other Custom Rule, it will match the Default Rule in the end**.

You can find this feature in the **Profile Options** section. 

![](https://files.readme.io/e9eebf8fd04830cb273d603f4a4bdf7fc750997fb2ed98d465c5b3fbc607b928-image.png)

## Rule Actions

Much like with standard Custom Rules, one of 3 actions can be chosen.

### Block

A BLOCK action will prevent all domains from loading, that did not match any Service or Custom Rule. This is best used to create highly restrictive access policies where only whitelisted domains or Services will actually load. You probably shouldn't do this unless you have an extensive "allow list". 

### Bypass

A BYPASS rule is the default action, which will resolve a domain to its true IP address from Authoritative DNS. If you're using [Multiple Enforced Profiles](doc:multiple-enforced-profiles), this is the anchor for your second profile to be enforced. 

### Redirect

A REDIRECT rule will spoof all domains to a proxy location or specific IP address chosen by you, **as long as they didn't match any of the Filters, Services or Custom Rules**. This will mask the client's source IP address for all browsing activity (that uses DNS). 

> 🚧 Use With Extreme Care
>
> **Redirecting all traffic can break some services such as SSH, games, VOIP apps, some messaging apps, and more.** Use this option with great care. You should BYPASS your favorite services (or domains via custom rules)  if you wish for them to see your true location (IP), or prevent them from breaking if they use non-standard protocols. 
>
> This feature can break [in certain scenarios](doc:ip-mismatch-between-dns-and-proxy). Do not enable it unless you know what you're doing.

## Redirect Modes

A redirect rule can be set to one of two modes:

* **Auto** - This will route your request to the closest Control D anycast location, and exit the request there. End-to-end IPv6 is supported. **This mode will have the best performance, and is recommended.**
* **Manual** - You can optionally specify the city where you want your traffic to exit. This performs a "double hop" from the closest Control D  (Auto) location to the chosen city. This mode will be slower, and does not support IPv6 end-to-end.
