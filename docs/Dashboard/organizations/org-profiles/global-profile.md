---
title: Global Profile
excerpt: Assign a common Profile to your sub-organizations and avoid policy duplication
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This feature builds on top of [Multiple Enforced Profiles](doc:multiple-enforced-profiles) functionality and allows Organization account users to set a Profile for the entire organization. This Profile will apply to all devices created inside this Sub-Organization. 

# How it works

Create or edit an existing Sub-Organization and choose a Global profile from the down-down menu. 

<Image align="center" width="55% " src="https://files.readme.io/b4adfa7e619b179aa28f5dbb3c45f6bcdc77d0a3be840c8c209ac56db597cc54-Global_Profile_Modal.png" />

Such a profile should (ideally) be common to many sub-organizations, so you can keep your "default policy" all in one place. Such a Profile/policy can:

* Block Malware as you probably want to do this inside of all Sub-Organizations
* Block common Services that none of your customers should access (ie. TikTok)
* Have special custom rules that are relevant to all Sub-Organizations 
* Create a common [Custom Block Page](doc:blocked-query-response)

Now, when you create a Device inside a Sub-Organization, and select a Profile that's specific to this Sub-Organization, the Global Profile will be automatically inherited, and enforced at the same time as your Organization specific profile. 

Be mindful, the same Global Profile cannot be selected as a Device specific Profile inside a sub-organization, as it's already enforced. You must choose another Sub-Organization specific or [Org: Shared Profile](doc:shared-profile). 

## Rule Priorities

The rule engine works as follows:

1. Custom rules take precedence over everything. 
2. Service rules are second in line, and are checked if there are no custom rules that match the DNS query. 
3. Filters (which block things) are 3rd in-line and will match a domain if there is no overriding custom rule or Service rule
4. Last in line is the Default Rule, which will, like the name suggests, match queries that aren't affected by any of the above

## Conflicts and Overrides

By default, if there is a conflict for the same Filter, Services, Custom Rule, or Profile Option, the Global Profile will win. For example, if *Gaming* is blocked in the **Global Profile**, but allowed in the **Sub-Organization Profile**, *Gaming* sites will still be blocked. Same is true for Services, if *TikTok* service was explicitly allowed (Bypassed) in the Global Profile, but blocked in the Sub-organization profile, it will still be allowed. 

You may not want this, in which case you can override the Global Profile, and have the Sub-Organization rule selection take precedence. In the Gaming Filter scenario presented earlier, you would see something like this when you view the Sub-Organization Profile.

<Image align="center" src="https://files.readme.io/13897e067867a4c9f44e6cf8a49dfd8b77986e5fae8eae27fb4e6dcd6ff61575-Overrides_Visible.png" />

Notice the yellow warning next to the Games filter. This suggests that this scope is blocked in the Global Profile. If you toggle this filter OFF, it will turn red, meaning it's overriding the Global Profile. 

<Image align="center" src="https://files.readme.io/f20cc0cd6bf2e543f8d46f439bef39987ca312ff8080b810ee02945e360e94f7-Overridden.png" />

Now, all devices in this Sub-Organization, that enforce this Sub-Organization Profile, will be allowed to access Gaming sites.
