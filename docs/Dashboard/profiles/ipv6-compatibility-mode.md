---
title: IPv4/IPv6 Compatibility Mode
excerpt: Redirect A records via IPv6 resolver and vice versa.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This option only has impact in the traffic redirection context (when you redirect a domain, service or all traffic) **and** when you have IPv6 enabled on your network. 

By default (with this option OFF), Control D will only respond with A records when you use IPv4 stack to communicate with the DNS resolver. If you're communicating to the DNS resolver via IPv6, Control D will only respond with AAAA records. Cross-stack records will not be returned. 

When this option is enabled, Control D will respond with A and AAAA records, regardless of the IP stack you're using to communicate with the DNS resolver. This can sometimes resolve some issues on mobile networks, but can also create issues for you if you just blindly enable this option. 

**Rule of thumb**: leave this option disabled unless instructed to enable it by Support.
