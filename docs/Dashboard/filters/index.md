---
title: Filters
excerpt: Filters block categories of websites, content and other scopes.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 📘 TLDR
>
> Filters are blocklists. Toggle them ON and everything in that category will be blocked on Endpoints that enforce the Profile.

# What are Filters?

Filters prevent websites and services that fall within the category from resolving on your device. There are 2 categories of Filters:

1. Native Filters - These are hand curated Filters maintained by Control D. These are highly effective in terms of the capabilities but should contain very few false positives.
2. 3rd Party Filters - These are popular community maintained blocklists. Control D does not control their contents and these should be used at your own risk.

<Image align="center" src="https://files.readme.io/0748bee985847b0262c3992e3b9a625edc896a5fad4050c107ba04a072b23e50-Filters_New_UI.png" />

## Modes

Some Filters have multiple modes, these Filters include:

* Ads & Trackers - See [Ads & Trackers Modes](doc:ads-filter-modes)
* Malware - See [Malware Modes](/docs/malware)

To learn more about each mode, you can click the Info icon next to the relevant Filter.

# How to Use Filters

To enable a Filter, simply toggle the relevant switch ON in the Profile you're editing. To disable a Filter, toggle it OFF.

If you'd like to enable (for instance) the `Social` Filter to block social media sites, but still enjoy Facebook, you can enable the `Service` for Facebook and it will work while the others will be blocked.

# Update Interval

All Filters are rebuilt and deployed every 15 minutes or less.

# Filter Name to Filter PK Mapping

When using our API, you might notice internal keys for Filters don't match perfectly with the names. Here is the mapping: 

| PK           | Name                    |
| ------------ | ----------------------- |
| ads          | Ads & Trackers          |
| porn         | Adult Content           |
| noai         | Artificial Intelligence |
| fakenews     | Clickbait               |
| cryptominers | Crypto                  |
| dating       | Dating                  |
| drugs        | Drugs                   |
| ddns         | Dynamic DNS             |
| filehost     | File Hosting            |
| gambling     | Gambling                |
| games        | Games                   |
| gov          | Government Sites        |
| iot          | IoT Telemetry           |
| malware      | Malware                 |
| nrd          | New Domains             |
| typo         | Phishing                |
| social       | Social                  |
| torrents     | Torrents & Privacy      |
| urlshort     | URL Shorteners          |
| dnsvpn       | VPN & DNS               |

<br />
