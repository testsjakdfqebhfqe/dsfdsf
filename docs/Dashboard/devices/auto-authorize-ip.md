---
title: Authorize by Secure DNS
excerpt: Authorize networks after successful Secure DNS queries.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
# What is Authorize by Secure DNS

Authorize by Secure DNS lets Control D authorize a network after a successful Secure DNS query from this Endpoint. When enabled, newly seen source IPs from Secure DNS usage can be stored with the Endpoint as Authorized IPs.

## How to Use

Edit an Endpoint and toggle **Authorize by Secure DNS** ON. When the Endpoint is used with a Secure DNS protocol, Control D can authorize the source network for that Endpoint.

<Image align="center" width="100%" title="authorize-by-secure-dns.png" alt="Authorize by Secure DNS setting in the Endpoint Advanced Settings dialog" src="https://files.readme.io/7d15e8fc483219162b02fae5872d604cab5860f570760795b01794b18f1566c6-authorize-by-secure-dns.png" />

If you have Legacy DNS enabled, stored Authorized IPs can use the Endpoint's Legacy DNS resolvers. Disabling this setting stops Control D from learning new IPs from Secure DNS usage.

> 🚧 Require Authorized IPs
>
> If **Require Authorized IPs** is already enabled, unknown IPs are refused before they can be learned. Add the IP manually or use another bootstrap method before requiring Authorized IPs for a new network.
