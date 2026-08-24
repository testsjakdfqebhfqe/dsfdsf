---
title: Check if DNS is working
excerpt: How to know that Control D is working, and what to do to fix it if it's not.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Quick Check

On a device that is supposed to be using Control D, simply visit the [Status Page](https://controld.com/status). It will tell you if you're currently using Control D or not. If you are, stop reading now, you're good to go. 

If it shows you're not using Control D, but you configured it, let's continue. 

## Command Line Check

If you've configured Control D on your network router, or directly on the network interface Control D should be setup OS wide. Open Terminal / command line and run this command: 

```shell
nslookup verify.controld.com

Server:         127.0.0.1
Address:        127.0.0.1#53

Non-authoritative answer:
verify.controld.com     canonical name = api.controld.com.
Name:   api.controld.com
Address: 147.185.34.1
Name:   api.controld.com
Address: 2606:1a40:3::1
```

* If this command return an IP address, your OS is in fact using Control D and the issue is with your browser using DNS-over-HTTPS, which overrides your DNS settings. Simply [configure DNS-over-HTTPS in your favorite browser](/docs/browser-not-using-os-dns) using the tutorials and the issue will be solved. Status page will give you instant feedback on your successful DoH setup. 

* If the `nslookup` command does NOT return a valid IP, your OS is not querying a Control D resolver you may have setup on your machine or router. You should double check your settings to make sure you've done this correctly.

## External Check

If your device does not have a browser, nor a command line, the only way you can check if Control D is working is to start the [Activity Log](/docs/activity-log) on a [Device](doc:devices)  that you've setup on your physical gadget. If you see any records in the Activity Log as you perform actions on the device, it's all working. If the log is always blank, then your DNS queries are not making it to Control D. The most likely reason for this is the fact that the [IP is not authorized](doc:ip-not-authorized).
