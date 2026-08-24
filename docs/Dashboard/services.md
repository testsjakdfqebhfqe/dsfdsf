---
title: Services
excerpt: Control individual websites, services and apps.
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
> Services are pre-made collections of domains that are used by various websites, apps and platforms. Block or Redirect them with a single click.

# What are Services

A service is a collection of rules that cover a website, app, or web service. A rule can be assigned to a Service, that will perform some type of action. Services are broken down into several categories. 

![](https://files.readme.io/77308ae427b85069348b0f73f77d83ab1fd1f02a7c999266cc1e374c3c753dc2-image.png)

<br />

## Service Rules

There are 3 types of rules that can be chosen for any specific service. 

![](https://files.readme.io/a4c0b287a66f514b4b4cdf957c33c915c85301eb8e4ba06a9b40c67b96c21ed1-image.png)

<br />

> 🚧 Matching Order
>
> Service rules override Filters. So for example, if you enabled the Social Filter (which blocks ALL social networks) you can use the Service rules to override this behavior and make selected services work (via BYPASS or REDIRECT rules).

### Block

The Block rule will prevent the Service from loading, and will effectively make it inaccessible from an Endpoint that enforces a Profile that blocks a specific service. 

### Bypass

The Bypass rule will resolve all domains associated with a Service to their true IPs. This is useful to override Filter blocks, or the Default Rule. 

> 📘 Rule OFF vs Bypass
>
> You may be wondering, what's the difference between setting a BYPASS rule vs disabling the service status toggle. If you have Default Rule set to BYPASS, there is no difference between the earlier mentioned Service rule settings - they will behave the same way (resolve Service normally). 
>
> If you have Default Rule set to Redirect, however, then the Service rule will override this behavior. A BYPASS rule will cause the Service to resolve normally (not be redirected).

### Redirect

The Redirect rule will spoof all domains related to a Service via a proxy location or specific IP address chosen by you.
