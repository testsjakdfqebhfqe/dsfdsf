---
title: Expose IP via DNS
excerpt: Advertise source IP of last Secure protocol query via a Dynamic DNS record.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
This is a unique feature that allows Control D to function as a Dynamic DNS service when you use a Secure DNS (DNS-over-HTTPS/TLS) supporting Device.

# What is Dynamic DNS?

Your home IP is usually dynamic, meaning it can change at any time, in many cases multiple times a day. If you have services hosted at your house (Plex server, NAS, BitTorrent client, etc) and you wish to reach them externally, you must know what your current IP address is. Traditionally, you would use a DDNS service that runs a piece of software on your network, or it may be directly built into your router. When your IP changes, it would notify a 3rd party DDNS service, which would then update a DNS record that points to your IP. This allows you to reach your home server via an easy to remember hostname, instead of a randomly changing IP address.

## Issues with DDNS Services

There are multiple downside to existing DDNS services, these include:

1. Your router may only support a small handful of DDNS services (usually zero or one). If you want to use another one, you cannot.
2. If you don't use a router, you have to run software on some device on your network.
3. The IP update interval is usually at least 60s (usually a lot more), so there will be outages when your IP changes.

Using Expose IP via DNS solves all these problems.

# How This Works


<Image src="https://files.readme.io/fcffb067f8f8bfb30de0c5327864c8c2ee0a6a320f8f4f1e351c44ed183b2538-expose-ip-via-dns.png" align="center" width="100%" />


1. Create a new Device or edit an existing device that is already configured on your network.
2. In the “Expose IP via DNS”, choose a subdomain you wish to claim for yourself and press Save.
3. Your personal DDNS Hostname will now be shown to you.

When a DNS query is made through this Device, the source IP will be reflected as an A or AAAA record on your personal Hostname.

```
test@Desktop:~$ dig whatever.controld.live

; <<>> DiG 9.11.3-1ubuntu1.15-Ubuntu <<>> whatever.controld.live
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8138
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 13, ADDITIONAL: 27

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;whatever.controld.live.      IN      A

;; ANSWER SECTION:
whatever.controld.live. 20    IN      A       104.168.34.156
```

This has the following advantages:

- Any router or device that supports DNS-over-HTTPS or DNS-over-TLS can update your IP simply by making a DNS query.
- There is no software or scripting required. Although you can totally script a manual DNS-over-HTTPS/TLS resolution using your Device specific resolver, same way you would make an API call against a traditional DDNS service.<br />Most networks are very chatty, and DNS queries are made constantly, so this will update your IP almost instantly.
- There is no update interval to wait for.

<br />
