---
title: IP Management
excerpt: View IPs that queried a device/endpoint, or are authorized to use it.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is IP Management

This feature is optional depending on what types of Devices/Endpoints you use, and what your privacy criteria is. This web control panel section allows you to view IPs that have interacted with your Device/Endpoint solvers, or restrict what IPs that are allowed to communicate with them. 

## How to Use

From the **Endpoints** section, select this icon;

<Image title="view_ips.JPG" alt={884} align="center" width="100% " src="https://files.readme.io/39155fb8bf9fa9a05264fc167ed3f48d8ba17233265a4016d3e2db2f24632deb-IPs_from_Endpoints_Area.png" />

Depending on your Device/Endpoint Settings, this will either show you nothing, or a list of IPs that have interacted or are allowed to interact with your Device/Endpoint specific resolver:

<Image align="center" src="https://files.readme.io/8132410fd1d01665c8b2a9d236b769554396fa2176a4c6ed7f28c0884942d615-IPs_Area.png" />

### Secure DNS Only

If your Device uses Secure DNS protocols, you can Disable the [Auto Authorize IP](/docs/auto-authorize-ip) feature, which will prevent source IPs from being logged on that page. 

### Legacy Resolvers

If your Device requires [Legacy DNS Resolvers](/docs/legacy-resolver), the IP logging feature cannot be disabled, as the meaning of it changes. It now functions as a list of IPs that are allowed to interact with your Legacy DNS resolver. 

## Delete IPs

From the listing page, you can de-authorize or remove any IP address you see.
