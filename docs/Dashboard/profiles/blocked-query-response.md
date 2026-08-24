---
title: Blocked Query Response (Custom Block Pages)
excerpt: Customize how Control D responds to blocked queries.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is this?

When Control D blocks a domain via a Filter, Service, or Custom Rule, by default it returns the following DNS records:

* A: `0.0.0.0`
* AAAA: `::`

This feature allows you to change this behavior and return a different response.

# How to Use it

Edit your desired Profile and go to **Profile Options**. 

<Image align="center" src="https://files.readme.io/aa0be69bd9fd51c08d1e493ead4e9a8c61bc6bcde8cf1e6122a945c787a5131c-Block_Response.png" />

Toggle this feature ON and choose the desired response type. There are several to choose from:

* `0.0.0.0 / ::` (Default)
* `NXDOMAIN` - Return this RCODE
* `REFUSED` - Return this RCODE
* `Custom` - Choose your own IPs to respond with or use custom block page
* `Branded` - Use a branded and customizable block page

## Custom Block Page

Here you can input your own IPv4 and IPv6 addresses. When a website is blocked, Control D will spoof to IP addresses you have chosen here. This can be used with a self-hosted block page + your own Root Certificate. 

<Image align="center" src="https://files.readme.io/8d08adcece9dd2261e13f22154fa3e55c4834eb6a6edc176573e1c6cd66f9190-Custom_Block.png" />

## Branded Block Page

> ❗️ Root Certificate Installation Required
>
> In order for this to work with HTTPS websites, [Root Certificate Installation](doc:root-certificate-installation) is required. Check the linked document to learn more.

This option allows you to use a Control D hosted block page, which you can optionally customize with:

* Your own logo
* Custom block title
* Custom block message
* External link title
* External link URL

By default, with no custom settings, a branded page will look like this. 

![](https://files.readme.io/d4d3324-image.png)

Now, you can customize it using the 5 fields.

![](https://files.readme.io/9fd64123ca360ccba46f0f4aa1eab2c70d83377a08d3a9a4fa74b3d744c58f66-image.png)

When a website is blocked, it will look something like this. 

![](https://files.readme.io/e729e22-image.png)

### Unblock Request Button

You can choose whether to show a Request Unblock button on a branded page using the Unblock Reporting dropdown which provides 3 options.

* None - No button will be shown

<Image align="center" width="100% " src="https://files.readme.io/8c1da224d9a586fe935ec2c97c916c7e79ade076da4f7cc7bca0bcec92d552c8-image.png" />

* Default - A Request Unblock button will be shown.  Clicking this button will reveal a small form where the end user can request for this page to be unblocked. The account owner or admin will receive this request via email or Slack notification, and an action can be performed.

![](https://files.readme.io/068ccac75bccd6d88507970d37ac66ffdff42443c2f739bb3c78648ffba80820-image.png)

* Custom - The External Link Title and External Link URL fields will allow you to customize what the button says and does.

<Image align="center" width="100% " src="https://files.readme.io/709b57c3778ddf6023f631c796b7cee96cbfcdd154763506bbf9e486134cc715-image.png" />

### Unblock Request Handling

By default, the organization owner or admin receives unblock requests via email. If you prefer to send these requests to a specific set of email addresses or a Slack channel (via a webhook), you can configure this on the My Org page.

Go to My Org and enable the Unblock Reporting option. Then, add your desired email addresses and/or Slack webhook URL, and click Save. From that point on, all unblock requests will be sent to the specified email list and/or Slack channel.

![](https://files.readme.io/ab5480ba766ac5b65df39920c39916af58e0e6dae6510140a661ebe2e1758ae4-image.png)

#### Unblock request email/Slack priority handling

When an unblock request is submitted, Control D determines who should receive the notification based on two factors:  

* Which Organization owns the endpoint (parent vs. Sub-Organization)  
* Whether custom recipients are configured  

The rules are as follows:

| Endpoint ownership      | Custom recipients defined | Notification goes to                                                 |
| ----------------------- | ------------------------- | -------------------------------------------------------------------- |
| **Parent Organization** | Yes                       | Parent Organization custom recipients                                |
| **Parent Organization** | No                        | All parent Organization admins                                       |
| **Sub-Org**             | Yes                       | Sub-Organization custom recipients                                   |
| **Sub-Org**             | No, but parent has them   | Parent Organization custom recipients                                |
| **Sub-Org**             | No (and parent has none)  | All Sub-Organization members **and** all parent Organization members |

## Hostname Variable

In the **External Link URL** you can use a variable `{domain}` which will template your link with the website FQDN that was blocked. For example, if you use: `https://reporting-url-example.com?hostname={domain}` and access pornhub.com, and it's blocked, the link will become `https://reporting-url-example.com?hostname=pornhub.com`

<Callout icon="🍎" theme="default">
  ### If the physical device in use is an Apple platform, the Shortcuts url scheme can be used as the link on the branded block page.

  Using this neat trick, a shortcut can be built to send pertinent information to the “family IT admin” along with something like "I need something unblocked," all in the background.
</Callout>
