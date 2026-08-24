---
title: Control D for Business
excerpt: >-
  Secure your whole network and individual employee devices in just a few
  minutes. Really.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Stop thinking about DNS

![](https://files.readme.io/c0f8f9c-image.png)

You may have used other commercial DNS filtering platforms, or even something like Pi-Hole, or AdGuard Home. Here is why they fall short:

* Most don't support modern (encrypted) DNS protocols - security services over UDP53 is crazy!
* Don't work on mobile devices without apps (or Wireguard tunnels)
* Require constant effort to keep running
* Look and function like they were built in the 90s
* Require extensive knowledge of the documentation (who likes reading a 500 page guide for a website UI?)

Control D was built in 2023 (and is actively updated and maintained), leveraging modern DNS protocols (legacy too), while natively supporting all types of devices, with optional (and [open sourced](https://github.com/Control-D-Inc/ctrld)) roaming clients. 

## All Platforms

Control D can be deployed on any Internet connected device, including but not limited to. 

* 🖥️ Windows
* 💻 Mac
* 🐧 Linux
* 🍎 iOS
* 🤖 Android
* 📡 Routers

## Modern Protocols

<Image align="center" src="https://files.readme.io/80c9a91-Modern_Protocol.png" />

Control D supports all DNS protocols you can think of, including bleeding edge ones like DOH3. 

* DNS-over-HTTPS
* DNS-over-HTTPS/3
* DNS-over-TLS
* DNS-over-QUIC
* Legacy DNS (UDP 53)

# 🚩 Problem -> Solution

Here are some problems you can solve with Control D, in as little as 10 minutes. 

## 🔒 Secure End User Devices

<Image align="center" src="https://files.readme.io/f459695-Secure_End_User_Devices.png" />

Protect your staff from malicious attacks, phishing and harmful online content with a handful of clicks. Bad things can’t reach their device if they don’t resolve.

* ✅ Roaming clients for all OSes
* ✅ Compatible with most RMM/MDM platforms

## 🛡️ Protect Whole Networks

<Image align="center" src="https://files.readme.io/97ad1d9-Protect_Whole_Networks.png" />

Safeguard against threats before a connection is even made. Block malware, cryptojacking and phishing domains across entire networks by deploying Control D on a router.

* ✅ Bespoke domain and IP level blocklists
* ✅ Machine learning based filtering

## 🚧 Block Unwanted Content

<Image align="center" src="https://files.readme.io/30a1572-Malware.png" />

Ads, clickbait, social media and porn can be harmful to the productivity of your business. Block unwanted content across networks, or on individual devices with a single click. Create blocking schedules to for dynamic behaviors.

* ✅ 20+ filtering categories
* ✅ 400+ individually blockable services

## 📈 Gain Actionable Insights

<Image align="center" src="https://files.readme.io/f99ae35-Gain_Actionable_Insights.png" />

**Optionally** log every DNS query, from every device and gain insights on the activity of your end-users and whole networks.

* ✅ View historical statistics
* ✅ Choose jurisdiction where your data is stored

## 🕵️ Regain Privacy

<Image align="center" src="https://files.readme.io/7ab69a7-Regain_Privacy.png" />

Privacy and security go hand in hand. Block ads and trackers that can be used to spread malware via a single click and mask your IP from some or all websites you visit.

* ✅ Reduce page load times by blocking ads & trackers
* ✅ [Mask your location without a VPN](@default-rule)

# 🥕 Features

If you've already used the Consumer version, you're familiar with the core features (if you're not - [get a free trial](https://controld.com/plans?step=account\&fullControl=true)). **Here's what else is included in the Business accounts offering.**

## 👥 Multi-User Access

<Image align="center" src="https://files.readme.io/81e383a-Multi-Admin_Access.png" />

Manage your assets as a team. Invite an unlimited amount of team members, and assign them different permissions to be able to view or modify your Profiles (policies) and Endpoints (resolvers that enforce policies). 

[Learn more about Permissions](/docs/org-members-permissions). 

## 🏢 Sub-Organizations

<Image align="center" src="https://files.readme.io/526783e-Multi-Tenancy.png" />

Group your Profiles and Endpoints into organizational units, intuitively called "Sub-Organizations". These can be anything: physicals sites, departments, customer companies, or whatever you want. Delegate access to team members to manage the assets within each sub-organization. 

[Learn more about Sub-Organizations](/docs/org-sub-organizations). 

## 📲 Effortless RMM/MDM Onboarding

<Image align="center" src="https://files.readme.io/99a39d7-Mass_Onboarding.png" />

Looking to onboard hundreds of thousands of end-user endpoints without tearing what's left of your hair out, or reading unnecessarily verbose documentation that makes your ears curl? Good news, you can onboard as many endpoints as you want in minutes using your favorite MDM/RMM platform. All it takes is a single Powershell or Bash command that does it all. 

[Learn More about Provisioning](/docs/provisioning).

## 🛠️ API

Control D is an API first service. Our Dashboard is built around a public API. Use it to script any kind of behaviors you want, or even make your own custom white labeled control panel. 

[Check out the API Reference](/reference/get-started). 

# 📧 Talk to Us

Control D is in very active development, and you can talk directly to founders and developers on our subreddit or Discord. We're open to suggestions and improvement ideas, and ship new updates weekly. 

* [Reddit](https://www.reddit.com/r/controld)
* [Discord](https://discord.gg/dns)
* [Twitter / X](https://twitter.com/ControlDNS)
* [Email Us](mailto:hello@controld.com)
