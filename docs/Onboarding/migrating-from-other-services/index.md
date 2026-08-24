---
title: Migrating from Other Services
excerpt: >-
  Migration guides for moving DNS filtering, security, policy, and deployment
  workflows from other providers into Control D.
deprecated: false
hidden: false
metadata:
  robots: index
---
Each migration guide covers what to export from your existing provider, how to recreate the same general setup in Control D, and what to check before you fully switch traffic over.

## Available Migration Guides

* [Cisco Umbrella to Control D](doc:migrating-from-cisco-umbrella-to-control-d) — For teams moving policies, identities, roaming clients, and DNS forwarding from Cisco Umbrella into Control D.
* [DNSFilter to Control D](doc:migrating-from-dnsfilter-to-control-d) — For teams moving filtering policies, block lists, allow lists, organizations, and deployment workflows from DNSFilter into Control D.
* [NextDNS to Control D](doc:migrating-from-nextdns-to-control-d) — For teams moving profiles, filters, allow/deny lists, rewrites, client/router deployments, and logging preferences from NextDNS into Control D.

## Before You Migrate

Before changing production DNS, we recommend reviewing your current policies, identifying any required allow lists or block lists, and testing Control D with a small group of endpoints first.

After the new configuration is working as expected, you can move the rest of your users, devices, or networks over to Control D.
