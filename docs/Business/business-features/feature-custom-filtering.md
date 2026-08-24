---
title: Custom Filtering
excerpt: >-
  Granular control over individual domain names, where you can block specific
  websites, and even whole TLDs.
deprecated: false
hidden: false
link:
  new_tab: true
  url: https://controld.com/features/custom-filtering
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

Custom Filtering is a powerful feature within Control D that gives users fine-grained control over their network's domain access. It allows blocking of individual websites, entire top-level domains (TLDs), and the use of wildcard rules. [Custom Filtering](doc:custom-rules) also includes [Geo Custom Rules](doc:geo-custom-rules), which utilize geo-location data for more specific rule application.

# Problem Solved

Custom Filtering addresses the need for detailed filtering beyond general categories, or services, by allowing users to pinpoint specific domains or domain patterns they find objectionable or unsafe. Geo Custom Rules further enhance this by taking into account the geographical location of source and destination IPs.

# Feature Benefits

* **Granular Domain Control**: Directly manage access to specific domains or TLDs, giving exceptional precision in filtering decisions.
* **Wildcard Rule Flexibility**: Wildcards expand the capacity of rules, blocking a broader range of domains without needing to specify each one.
* **Geographical Considerations**: Geo Custom Rules block or allow content based on the physical location of the IP addresses, adding an extra dimension to access control.
* **Overriding Filters**: Custom Rules don't just block domains, they can also be used to override Filters in order to grant access to a blocked website or domain, or even redirect them via a proxy. 

# Using Custom Filtering

To employ Custom Filtering, users can create and enable rules in the [Custom Rules](doc:custom-rules) section of the web dashboard. Simply edit the desired Profile, and click on Custom Rules. By integrating these rules into your profiles, you can achieve a customized filtering policy that aligns with your specific security or compliance requirements.
