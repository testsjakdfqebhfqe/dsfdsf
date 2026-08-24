---
title: Browser not using OS DNS
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

Modern browsers like Google Chrome and Firefox can automatically enable DNS-over-HTTPS without your knowledge or consent. If this occurs, even if you changed your DNS servers inside your operating system, your browser will disregard it and keep using whatever DNS server is [configured in your browser](/docs/browsers-platform), or use both in parallel. 

# Problem

You configured Control D on your router using `ctrld`, or directly inside the OS using the app, but the web GUI and the [Status Page](https://controld.com/status) still say you're **not** using Control D, or you're getting unexpected behaviors (blocked sites are loading). The likely cause here is the fact that your browser is disregarding the DNS settings. 

# Solution

There are 2 ways you can resolve this issue. 

## Disable DNS-over-HTTPS

This may sound counter-intuitive, but this is the best solution. Simply disable DNS-over-HTTPS inside your browser. You can do this by opening browser settings, searching for "DNS", and disabling "Secure DNS" (in Chrome) or changing setting to "Off" (in Firefox).  

### Chrome

<Image align="center" src="https://files.readme.io/9fc4adb-doh_chrome.PNG" />

### Firefox

<Image align="center" src="https://files.readme.io/b51ad54-doh_firefox.PNG" />

 Your browser will now use your Secure DNS OS resolver, so your DNS queries would still be encrypted.

## Configure Control D in Browser

Alternatively, you can configure Control D directly in your browser, by [following this tutorial](/docs/browsers-platform).
