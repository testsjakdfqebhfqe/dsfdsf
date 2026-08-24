---
title: Connected Devices
excerpt: Physical devices that send DNS queries to Control D.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What are Connected Devices?

<Image align="center" width="55% " src="https://files.readme.io/b9a750cf044efb6a0be38072f41493e5f511eda859dfdb21d609d259ee824a15-Connected_Devices_New_UI.png" />

When you create a Control D **Endpoint**, it issues you a unique set of DNS resolvers, which you can configure to receive DNS queries from one or more physical devices used by humans. Some Endpoints are used by a single device, so feel free to put `1` into the box. 

Other Endpoints like AD domain controllers, routers, or DNS servers are used by multiple physical devices (phone, laptop, etc). So, if 100 devices are going to be sending their DNS queries to Control D, via this Endpoint, you need to put `100` into this box. 

## Honor System

We ask you to do your best to keep this count in sync with your actual usage. The amount of Connected Devices you select is not a hard limit, and nothing technically prevents you from putting `5` into the box, and using Control D on a network that has `5000` devices. However, we ask you to be fair and reasonable, since your honor is at stake. 

We perform periodic audits, and check if everything looks reasonable given the average volume of DNS queries that a physical device emits on a daily basis. If you're off by a little, we probably won't care. But if you're off by a lot, we'll know and contact you. 

<Image alt="You don't want us to send you an email like this" align="center" src="https://files.readme.io/fa57705-image.png">
  You don't want us to send you an email like this
</Image>
