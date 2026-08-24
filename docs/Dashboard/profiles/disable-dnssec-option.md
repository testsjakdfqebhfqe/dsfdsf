---
title: Disable DNSSEC
excerpt: Turn off DNSSEC validation for compatibility.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This feature disables DNSSEC. This is useful if you find that some websites don't resolve, usually due to misconfiguration on the part of the owner of the domain. The issue would present itself as follows:

![](https://files.readme.io/3955165-dnssec.PNG "dnssec.PNG")

To solve this issue, Edit your **Profile**, go to **Profile Options** and toggle the **Disable DNSSEC** Profile Option to ON.

<Image align="center" src="https://files.readme.io/03664d89e930c9a8b83605a36318f9d1eef9c7923a28c3282fcf8f132c38d6b6-DNSSEC.png" />

## Is this safe?

Yes, if you use Secure DNS protocols like DNS-over-HTTPS or DNS-over-TLS, DNSSEC provides virtually no value. Your DNS requests cannot be intercepted or spoofed by anyone.
