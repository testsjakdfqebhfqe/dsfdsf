---
title: Status Page
excerpt: What are all these Status page rows? Let's find out.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is the Status Page

The [Status Page](https://controld.com/status) is your one stop shop for all troubleshooting efforts. It provides ([almost](doc:high-latency-slow-speeds)) all relevant details we would need to troubleshoot any issue. If support instructed you to collect the info from this page, simply click the **Copy results** button at the top, and paste the results in the relevant thread.

> 🚧 Personal Information
>
> Do not post these results in a public place, as they will contain personal information like your IP address and your Endpoint ID. Only provide this to support in an email or other non-public means.

# What are all the sections?

## IPv4/IPv6 Address

These rows show what your current ISP assigned IPv4 and IPv6 (if available) addresses are, as well as your ISP and country. 

## Using Control D

This tells you if you're using a Control D resolver on the physical device viewing the page. If you see a red ❌, that means you're not actually using Control D. This will work for both free and premium DNS resolvers. 

## Resolver

This will tell you your Endpoint ID (the premium resolver you're using). If you're using the free DNS service, this will always be N/A. 

## DNS Protocol

If you're using a premium DNS resolver, this will tell you what DNS protocol you're using:

* Legacy
* DNS-over-HTTPS
* DNS-over-TLS
* DNS-over-QUIC

Free resolvers will always show N/A. 

## DNS Latency

This tells you the exact latency to the [closest Control D location](https://controld.com/network) that is serving your DNS traffic. If you ping dns.controld.com you should see approximately the same latency. 

## DNS Host

This shows you the hostname of a Control D server that is serving your DNS traffic. The first 3 letters will be an IATA airport code for the physical location. 

## DNS Source IP

This shows you the source IP as seen by the DNS server. In most cases this will match your IP address printed at the very top of the page. 

## Proxy Authorized

This tells you if your current DNS configuration is capable of redirecting traffic. If you see a red ❌ that means you either don't have any redirection rules in your enforced Profile, or something is wrong if you do have such rules, and they don't work. More on the solution below. 

## Proxy Latency

This is analogous to "DNS Latency", except it shows you the latency to the closest Control D location capable of serving redirected traffic. In some cases this will be identical to DNS Latency, but not always. 

> 📘 Higher Latency than DNS
>
> Every Control D location is capable of serving DNS traffic, but not every location can serve Proxy (redirected) traffic. If your closest DNS location is such a location, your proxy traffic will be sent to the next closest location that CAN serve it. Sometimes this location can be a lot further away, and have much higher latency.

## Proxy Host

This is analogous to "DNS Host", except it shows you the hostname of a Control D server that is serving your Proxy (redirected) traffic. The first 3 letters will be an IATA airport code for the physical location. 

## Proxy Source IP

This is analogous to "DNS Source IP", except it shows you the source IP as seen by the Proxy server. In most cases this will match your IP address printed at the very top of the page, but this may not always be the case. 

> 🚧 Different IP from DNS Source IP
>
> If you see that this IP differs from DNS Source IP, this is an unusual situation, but can happen on some cellular networks that use IPv6. If you're not redirecting any traffic, then the mismatch is of no consequence. If you are redirecting your traffic, this mismatch can cause connectivity problems as this IP will not be authorized in the global firewall, and you will not be able to reach the proxy, so all redirected requests would fail. 
>
> There are 2 solutions to this problem if you happen to encounter it:
>
> 1. Disable IPv6 - this will solve the problem, but may not be possible on some cellular networks. 
> 2. [Manually authorize](doc:ip-management)  the mismatched IP.

## New IPv4/IPv6 Address

If you're using [Default Rule](doc:default-rule) in Redirect mode, you will be assigned a Control D IP address that is visible to all websites and services you use, instead of your true IP at the top of the page. These rows will show you your new IP addresses (IPv4 and IPv6).
