---
title: Multiple Enforced Profiles
excerpt: >-
  Enforcing multiple Profiles on a Device can allow for highly complex
  behaviors.
deprecated: false
hidden: false
metadata:
  robots: index
---
Traditionally, a [Device](doc:devices) enforces a single [Profile](doc:profiles) (configuration). Control D also allows you to enforce multiple profiles on a single device, in order to create advanced rule matching behaviors. 

# How it works

![](https://files.readme.io/eb4ced1d58f993486a4c6dcec1116773e493d38a60511895d632c137d3c46539-image.png)

When creating a device, you can choose up to two Profiles (three for Organization accounts) that are enforced on the device. When you query a device that enforced 2 Profiles, the rule engine will merge the two profiles and look for any match. A match means:

* Filter was triggered that blocked something
* Service rule was triggered that blocked, redirected or bypassed something
* Custom rule was triggered that blocked, redirected or bypassed something
* Default Rule was triggered that blocked or redirected something

Multiple Profiles follow the same Rule Order as a single Profile would, so for example a Service will always override a Filter.

## Organization Accounts

If you have a Organization account, you can also leverage the [Global Profile](doc:global-profile) feature within any Sub-Organization. This can add a 3rd layer, meaning you can enforce up to 3 Profiles on any Device.

## Limitations

1. **Enforced Profile 2** is not a Schedule-only Profile. It remains part of the Device's normal Profile stack whenever no Schedule window is active.
2. During an active Schedule window, the scheduled Profile replaces the Device-level Enforced Profile stack. Do not add a Profile as **Enforced Profile 2** if you intend it to apply only during a Schedule window; assign it directly to the window instead.

# Use Cases

There are many powerful behaviors that you can accomplish with this feature. Some of these include:

## Common Rules

You may have multiple profiles, but they probably have few/many rules that are common between all of them. If you change a rule in one, you have to go and manually change it in all other profiles. Instead, you can just have a single “Common Profile” that has all your common rules. Then your device specific profiles can have only the rules you need on those specific devices. So you can have something like this:

* Device A: Everyone Profile → Work Profile
* Device B: Everyone Profile → Home Profile
* Device C: Everyone Profile → Employee Profile

“Everyone Profile” contains things you probably want on all devices (block Malware, Ads, Phishing), while device/use-case specific profiles can only contain rules for things you only need on those specific devices. This eliminates the need to duplicate or sync rules. 

If you have a Organization account, and leverage sub-organizations you can make this 3 tiered:

* Device A: Global Profile For Entire Org → Support Department Profile → User Specific Profile  
* Device B: Global Profile For Entire Org → Marketing Department Profile → User Specific Profile
* Device C: Global Profile For Entire Org →  User Specific Profile

## Rule Priorities

The rule engine works as follows:

1. Custom rules take precedence over everything
2. Service rules are second in line, and are checked if there are no custom rules that match the DNS query
3. Filters (which block things) are 3rd in-line and will match a domain if there is no overriding custom rule or Service rule
4. Last in line is the Default Rule, which will, like the name suggests, match queries that aren't affected by any of the above
