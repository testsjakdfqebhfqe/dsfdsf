---
title: Profiles
excerpt: A collection of rules, sometimes known as a configuration or policy.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: Learn more about Devices and how to use them with Profiles.
  pages:
    - type: basic
      slug: devices
      title: Devices
---
> 📘 TL;DR
>
> Profiles are policies: collections of rules and behaviors you want to enforce on a set of physical devices. Profiles can be chained in order to reduce duplication and form complex behaviors.

# What are Profiles?

A Profile is simply a collection of rules and settings you wish to enforce on a specific resolver. This can sometimes be known as a policy or configuration. A Profile has the following elements that can be tweaked:

* **[Filters](/docs/filters)** - categories you wish to be blocked.
* **[Services](/docs/services)** - specific websites and services you wish to block or redirect.
* **[Custom Rules](/docs/custom-rules)** - granular domain level rules.
* **Profile Options** - customizable behaviors within a Profile.

<Image align="center" src="https://files.readme.io/722f28d1578166db33efb4a1aaa40f99ccf80bd99b5975d88abcb688dbab678a-Profiles2.png" />

## Policy Priority

If there are multiple rules for the same domain, the policy with the highest priority will override anything with a lower priority. The list below shows the priority order, with the policy at the top having the highest priority and the one at the bottom having the lowest priority:

1. **[Custom Rules](/docs/custom-rules)** 
2. **[Services](/docs/services)** 
3. **[Filters](/docs/filters)** 
4. **[Default Rule](default-rule)** - When no Custom Rule, Service or Filter matches a domain, the Default Rule comes into effect.

# How to Use Profiles

A Profile by itself doesn't do anything, it must be enforced on an **Endpoint** in order to be used. A single Profile can be enforced on one or more **Endpoints** (resolvers). 

## Multiple Profiles

For some people, a single Profile may be enough if you wish to enforce the same rules across all your devices. However it's much more likely that you want to enforce different rules on different Endpoints, since you probably don't do the same things on your work MacBook that you do on your personal phone, or Android TV box.  This is why it's handy to have use-case specific Profiles, for example:

1. Work Profile - Blocks Malware and anything that is distracting (social networks, games, Tinder, etc). 
2. Kids Profile - Blocks adult content and other things not appropriate for children. 
3. Personal Profile - Any collection of rules that you find useful for your own personal use cases. 

Each Profile is then enforced on a relevant Endpoint, which is configured directly on a physical gadget you may be using (MacBook, Android Phone, iPad, home router, etc).

## Profile Options

You can enable various Profile Options in the Profile Editor mode. To learn more about various Profile Options, see the **Learn More** link which describes them.

<Image align="center" src="https://files.readme.io/05dd7a29ef3fb8d7ad9c962a0216e2baf5a68936ba949310c5523c19667063fc-Profile_Options.png" />
