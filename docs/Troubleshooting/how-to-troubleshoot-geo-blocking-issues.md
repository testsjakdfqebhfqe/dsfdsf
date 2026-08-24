---
title: How to troubleshoot geo-blocking issues
excerpt: The more effort you put in, the more likely we're to fix the problem.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 🚧 Best Effort Use Case
>
> Control D is a security and productivity platform, **not a geo-unblocking service**. We don't mention this feature anywhere on our website and offer it on a best effort basis only. You should not signup to Control D if this is your primary use case (which is also mentioned on the signup page).

# What not to do

If something doesn't work, and you make a report that sounds similar to...

* "Service X doesn't work" 
* "Service Y on my phone is lagging and giving me errors"
* "Can you make service Z work thanks"

**... we will not take any action and ignore you. Sorry.**

# What to do

![](https://files.readme.io/2fd5973-image.png)

In order for us to look at the issue and fix it (when time permits), you need to make an effort to troubleshoot the issue yourself, collect the relevant logs, and let us know exactly what you tried and what you think the problem is. 

## Step 1 - Verify

Make sure the relevant Video service is actually redirected via a supported location, validate this using the [Activity Log](doc:activity-log). 

1. [Collect Activity Log](doc:collect-activity-log) - it's helpful to do this on a desktop computer
2. Fresh open app or website **on the affected device** and reproduce the issue
3. Watch the logs in real time

## Step 2 - Try Another Device

To rule out a global issue with the service (it's usually not), attempt to access the affected service in a desktop browser, while using the same Control D profile, that redirects this service. 

## Step 3 - Attempt Fix

If the service is actually being redirected, the most common issue is that the streaming service added a new domain name, which needs to be redirected through an appropriate location, but currently is not. This results in a failed geo-location check. 

1. In the Activity Log, look for "important looking" domains related to the service you're using. These could be CDNs, new geo-check methods, or anything that's not being redirected in a stream of DNS queries from the relevant service. 
2. Make custom rules and redirect those domains to the appropriate location. 
3. **Fully restart** the browser or app you're using to access the service after you made a rule change
4. If the issue is still not resolved, or you don't know which domains are "important", t**ry using[Default Rule](doc:default-rule) -> Redirect mode to the same location**, which will redirect all domains via relevant country (select exact country location, not Auto mode).

If these steps resolve the issue, send us the domains you redirected so we can add them to base Services rules, or the full Activity log. 

## Step 4 - Send Us Data

> 🚧 Don't skip to this step
>
> If you want us to attempt a solution, please perform steps 1-3 first.

If everything you tried failed, then the solution would be on our end, which would involve sending new domains you discovered via residential proxies (something *you* cannot do). In order for us to attempt this, you need to provide us with the following:

1. Exact service you're using (website, app, etc)
2. Affected device (desktop browser, mobile device, operating system, etc)
3. Steps you've taken to solve the problem - don't say "I tried everything", tell us what you did
4. List of "important" domains you discovered and/or full activity log 

Send this data to the [support team](https://controld.com/contact). We do not guarantee a solution, and will handle these types of requests on a best effort basis. The more info you provide, the higher the chance of us solving the problem.
