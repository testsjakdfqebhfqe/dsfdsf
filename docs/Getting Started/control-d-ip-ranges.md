---
title: Control D IP Ranges
excerpt: The following anycast IP ranges are used by Control D.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# DNS

These ranges are used to handle DNS queries, using any protocol, most commonly used ports are: TCP+UDP 53, 853, 443.

* `76.76.2.0/24`
* `76.76.10.0/24`
* `2606:1a40::/48`
* `2606:1a40:1::/48`

Primary endpoints (which should be used as Bootstrap IPs) for Secure DNS protocols (DoH, DOT, DoQ) are:

* `freedns.controld.com`
  * `76.76.2.11`
  * `76.76.10.11`
  * `2606:1a40::11`
  * `2606:1a40:1::11`
* `dns.controld.com`
  * `76.76.2.22`
  * `76.76.10.22`
  * `2606:1a40::22`
  * `2606:1a40:1::22`

> 👍 IP TLS Certs Available
>
> DNS-over-HTTPS endpoints can be accessed directly via their IP addresses (TLS will validate), eliminating the need to bootstrap.
>
> * [https://dns.controld.com](https://dns.controld.com) -> [https://76.76.2.22](https://76.76.2.22)
> * [https://freedns.controld.com](https://freedns.controld.com) -> [https://76.76.2.11](https://76.76.2.11)

# Proxy

These ranges are used for transparent TCP proxying, **on any port**.

* `206.253.88.0/22`
* `2606:1a40:2::/48`

# Web / API

These ranges are used by HTTP services, like the API, website, and static assets. Mostly on port 443.

* `147.185.34.0/24`
* `2606:1a40:3::/48`
