---
title: Require Authorized IPs
excerpt: Restrict an Endpoint to only respond to queries from authorized IPs.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
> 📘 Organizations Only
>
> A business account is required to use this feature.

# What is Require Authorized IPs

Under normal circumstances, your personal DNS resolvers for each Endpoint are accessible from any IP. This means that any IP on the Internet can query against your Secure DNS resolver, if they know your secret Resolver ID, and be subject to the rules of the enforced Profile.

The **Require Authorized IPs** setting locks down your Endpoint's resolver to only allow queries from IPs you've explicitly allowed. This is effectively the opposite of [Authorize by Secure DNS](doc:auto-authorize-ip). Any IP that is not seen in the [IP Management](doc:ip-management) section will get a REFUSED query response.

## How to Enable

Create a new Endpoint, or edit an existing one and toggle **Require Authorized IPs** ON.


<Image src="https://files.readme.io/2d23c2bed20941dfd26047e2308b3d1290f93c9058420ff7f74aa962297f327b-require-authorized-ips.png" align="center" width="100%" />


Next, head over to the [IP Management](doc:ip-management) section and add IPs that are explicitly allowed to use this Endpoint.

![](https://files.readme.io/a0e4df7ebc23db8fc6f02e70ae91d5a780bb8b1a3e768996c10e444112aa223a-image.png)

### Additional Notes

If you're using `ctrld` DNS daemon, and it's running on a WAN addressable IP, DNS query Analytics will not be logged unless Require Authorized IPs is enabled. **But you should definitely not run**`ctrld`**&#x20;on a publicly accessible  IP.**
