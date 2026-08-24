---
title: EDNS Client Subnet Options
excerpt: Support for Custom ECS. Advanced.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The ECS (EDNS Client Subnet) feature is an advanced tool for managing the behavior of DNS queries made through Control D. It appears as a toggle under **Profile Options** and is toggled off by default. Here's how this feature works and what each option means.  

![](https://files.readme.io/4b9625f9fb4308679898df69616499e886ddc08c76f9bd82ef4ad48a37ed48dc-image.png)

### What is ECS (EDNS Client Subnet)?

In simple terms, ECS is a way for DNS requests to include part of your IP address (specifically, the subnet) when they are sent to a DNS server. This helps the DNS server provide responses that are more relevant to your location, potentially improving speed and accuracy. However, it also means sharing part of your network information with upstream DNS providers.  

***

### ECS Toggle Options

When you toggle ECS on, you'll see three options in the dropdown menu:  

#### No ECS

This option functions identically to keeping ECS turned off, meaning no subnet information is included in the DNS requests. It's the most privacy-focused choice, as none of your IP address is shared with upstream providers.  

#### Auto

When this is selected, Control D will automatically use the subnet of the server that you are using for DNS resolution. This was the default behavior before the introduction of this new toggle (unless you had the Disable DNSSEC option enabled, which would disable ECS support). It gives the advantage of more location-relevant results, but without directly sharing your own subnet information.  

#### Custom

This option lets you provide a custom subnet that will be sent with DNS requests. This can be useful if you need to specify a particular location, or want to expose your actual client subnet.  

* **For  IPv4 records:** The custom IPv4 subnet will be used. If no custom subnet is configured, Control D will use the nearest Point of Presence (PoP)'s IPv4 subnet.  
* **For IPv6 records:** The custom IPv6 subnet will be used. If no custom subnet is configured, Control D will use the nearest PoP's IPv6 subnet.  

This fallback ensures that DNS resolution always "just works," even if custom subnets are not configured.  

***

### Default Setting

By default, the ECS toggle is Off, meaning no ECS information will be sent. This maximizes user privacy and avoids sharing subnet data.  

You can adjust these settings based on your preferences for privacy and DNS response relevance.
