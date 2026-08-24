---
title: Unable to resolve any website / No Internet
excerpt: >-
  If an endpoint that uses a Control D resolver is unable to access any website,
  there are a few things you can do to troubleshoot this.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
There are several reasons why this issue can occur, and it all depends on how you configured Control D, and on what type of physical device. 

## Deleted Active Device

> 🚧 Most Common
>
> If you delete an actively used Device / Endpoint from the web panel, while the associated DNS resolver is actively used on the physical device, you will lose all Internet, **as the warning screen suggests when you delete the device**. If our website (controld.com) loads, but nothing else does, then this is definitely the problem.

To fix the issue, simply remove the Control D DNS resolver from the device. This depends on how you installed it.

* If you used the `ctrld` DNS daemon - run `ctrld uninstall` command or simply restart the machine
* If you used the GUI app - open the app again, and click the Restore button

## DNS Hijacking

Some ISPs and corporate or school networks hijack Legacy DNS and redirect it to their own resolvers. If the client happens to be on such a network AND uses Legacy DNS, there is nothing you can do about this except switch to a Secure DNS protocol like DNS-over-HTTPS or DNS-over-TLS. 

## Routing Issues

If you're using Secure DNS protocols, there should be very few reasons for it not working, except for routing issues. Try pinging **dns.controld.com** and see if you get a response, if you do not, that suggests the IP is not routable from your network. This should be rare, but if it occurs, [send us a traceroute](/docs/high-latency-slow-speeds).

## Restricted Resolver (Organizations only)

Organization users may need to double check their [Restricted Resolver](https://docs.controld.com/edit/restricted-resolver) settings.
