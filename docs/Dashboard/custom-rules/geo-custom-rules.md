---
title: Geo Custom Rules
excerpt: >-
  You can create custom rules that leverage geo-location data of source and
  destination IPs.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 📘 Beta Feature
>
> This feature is in beta, and lacks a "pretty UI", however you can use it right now.

# What are Geo Custom Rules

Geo Custom Rules work exactly as standard (domain based) custom rules, except they leverage the geo-location data that's associated with the source IP that made a DNS query, as well as destination IPs that the query resolves to. Here are some examples of what you can do with these types of rules:

* Block queries that resolve to IPs in a specific country 
* Redirect queries that **don't** resolve to IPs in a specific country
* Bypass queries made from IPs in a specific country 
* Block queries made from IPs **not** in a specific country 

Or any combination of the above.

## Rule Format

Geo Custom Rules start with any of the 4 following formats, and are followed by a [2 letter ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). 

* `@` - destination country 
* `!@` - NOT destination country
* `@AS00000` - destination Autonomous System (AS)
* `!@AS00000` - NOT destination Autonomous System (AS)
* `#` - source country 
* `!#` - NOT source country

## Examples

Simply create a standard Custom Rule, but instead of a domain name use any of the following formats:

* `@CN` - This will match queries that resolves to a Chinese IP addresses.
* `!@US` - This will match queries that do **not** resolve to a US IP addresses.
* `@AS16509` - This will match queries that resolve to IPs that belong to AS16509 / Amazon.com
* `!@AS13335` - This will match quires that do **not** resolve to AS13335 / Cloudflare Inc
* `#CA` - This will match if the DNS query originates from a Canadian IP address. 
* `!#DE` - This will match if the DNS query does **not** originate from a German IP address.

You can use any [2 letter ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) to make country based rules. You can also make several of these rules in one go, by listing them one per line while adding custom rules (same as domain level rules). 

Rules for ASes have a prefix `AS` followed by the AS number. **AS based rules supersede country based ones.**

> 🚧 NOT Rules Limitations
>
> You should not mix different **Rule Actions** for the "not rules" (the ones that start with `!`), or unexpected behavior will occur. See below for some examples.

### This OK

* `!#US` -> BLOCK 
* `!#CA` -> BLOCK

The above will result in DNS queries originating from US **and** Canada working normally (subject to the rest of your Profile), while queries that originate from all other countries would get a BLOCK response. 

### This is NOT OK

* `!#US` -> BLOCK 
* `!#CA` -> BYPASS

The above is NOT OK to do. Unexpected (random) behavior will occur. The exact same thing is true for `!@` (destination)  rules. 

## Rule Actions

Much like with standard Custom Rules one of 3 rule types can be attached to any geo custom rule. Be aware that **domain level rules take priority**, so if a query matches a domain level rule that will take precedence over any of your geo rules.

### Block

A BLOCK action will prevent any domain that matches a rule from loading, and will effectively make it inaccessible from a Device that enforces a Profile.  

### Bypass

A BYPASS rule will resolve any domain to its true IP address from Authoritative DNS. This is useful to override Filters, Services, or the Default Rule. 

### Redirect

A REDIRECT rule will spoof any domain via a proxy location or specific IP address chosen by you.
