---
title: Authorize by Dynamic DNS
excerpt: Scrape a DDNS hostname for IP changes and authorize Legacy DNS access.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
# What is Authorize by Dynamic DNS

Dynamic DNS (DDNS) is a method of updating a dynamic IP address using DNS. There are dozens of various DDNS services available, and you can use any one of them. Once you have your DDNS hostname that keeps track of your dynamic IP address, you can use it to auto-authorize your IP to work with Legacy DNS.

> 📘 Don't Forget
>
> If you use Legacy DNS, client source IP must be known to Control D in order for it to work. Secure DNS does not suffer from [this limitation](/docs/ip-not-authorized), and is the preferred method of using Control D.

## How to Use Authorize by Dynamic DNS

Simply edit one of your Endpoints that has a Legacy Resolver enabled that you actually use. Toggle **Authorize by Dynamic DNS**, and input your hostname. This hostname will be scraped at minutely intervals, and any IP that appears in this DNS record will be authorized to access your Legacy DNS resolver.


<Image src="https://files.readme.io/d7972d311e2516353c2a15c5382eb2f3f7b677d490ca7359a8206a1eeb18ffa0-authorize-by-dynamic-dns.png" align="left" width="100%" />


<br />
