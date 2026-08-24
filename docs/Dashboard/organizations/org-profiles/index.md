---
title: Profiles
excerpt: Think of these as policies.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: org-users
      title: Users
---
# What are Profiles?

A Profile is simply a collection of rules and settings you wish to enforce on a specific resolver (Device). This can sometimes be known as a policy or configuration. To view a list of all your Profiles, click the appropriately named Profiles button in the main nav bar. 

<Image align="center" src="https://files.readme.io/625cf39-policies.PNG" />

## Profile Components

A Profile has the following component that can be tweaked to fit your use case:

* **[Filters](/docs/filters)** - Categories you wish to be blocked
* **[Services](/docs/services)** - Specific websites and services you wish to block or redirect 
* **[Custom Rules](/docs/custom-rules)** - Granular domain level rules 
* **Profile Options** - Customizable behaviors within a Profile

<Image align="center" src="https://files.readme.io/b31854d-profile_editor.PNG" />

## Priority

If there are multiple rules for the same domain, the component with the highest priority will override anything with a lower priority. The list below shows the priority order, with the component at the top having the highest priority and the one at the bottom having the lowest priority:

1. **[Custom Rules](/docs/custom-rules)** 
2. **[Services](/docs/services)** 
3. **[Filters](/docs/filters)** 
4. **[Default Rule](default-rule)** - When no Custom Rule, Service or Filter matches a domain, the Default Rule comes into effect.

See the [advanced rules creation guide](doc:advanced-rules-creation-guide) in order to learn what advanced behaviors you can implement with these components. 

# How to Use Profiles

A Profile by itself doesn't do anything - it must be enforced on an Endpoint Device in order to be used. A single Profile can be enforced on one or more Endpoint Devices (resolvers).
