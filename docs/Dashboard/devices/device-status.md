---
title: Status
excerpt: Current state of the device/endpoint.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
# Device/Endpoint Statuses

This Device Setting allows you to control the status of a Device, and can have one of several options.


<Image src="https://files.readme.io/5eebdef76bf4ca4a6e7d224c764981f971ef70d1e631cd6ec77e3c364420d8db-device-status.png" align="left" width="100%" />


## Pending

This status means a Device/Endpoint has never been used. As soon as it's configured on a physical device, and a single DNS query is made against it, it will flip to the Active state.

## Active

A Device/Endpoint that is currently used or was used at some point in the past.

## Soft Disabled

Chosen Profile will no longer be enforced on this device/endpoint. It will function as a standard DNS resolver, not blocking or redirecting anything.

## Hard Disabled

Device/endpoint is disabled, and will not serve any DNS queries. If it's configured on a physical device, Internet access will be disabled.
