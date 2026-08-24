---
title: CNAME Flattening
excerpt: >-
  Control D supports CNAME Flattening as a Profile Option, allowing you to
  simplify DNS responses by replacing long CNAME chains with a single A/AAAA
  record.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## What Is CNAME Flattening?

When enabled, **CNAME Flattening** modifies upstream DNS responses that contain a chain of `CNAME` records ending in an `A` or `AAAA` record. Instead of returning the full chain of CNAMEs, Control D responds with a **flattened** answer: a single record that maps the original query name (`QNAME`) directly to the resolved IP address.

This feature is especially useful when:

* You want to reduce DNS resolution steps on the client side  
* You're serving records to systems that don’t handle CNAME chains well  
* You want more control over how DNS responses are returned

***

## How to Enable

CNAME Flattening is configured at the profile level:

1. Go to [Profiles](https://controld.com/dashboard/profiles).
2. Select the Profile you'd like to modify.
3. In the **Profile Options** section, enable **CNAME Flattening**.

***

## Notes

* If the upstream response does not contain a valid A/AAAA record at the end of the CNAME chain, no flattening occurs.
* Flattening is done per query; results are cached according to TTL.
