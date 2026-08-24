---
title: Update IP via Heartbeat Device
excerpt: How to automatically update IPs using a browser and DNS-over-HTTPS.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
If you're forced to use Legacy DNS on your router, and unable to use the [Command Line Daemon](doc:ctrld) which eliminates the need to do any of the following, then your best bet is using a Heartbeat Device. 

# What is Heartbeat Device

If you recall, when you use Secure DNS protocols like DNS-over-HTTPS/TLS/QUIC your source IP doesn't matter, Control D will just work regardless of what your IP is, and how often it changes. You may not be able to use these protocols on your router, but if you have desktop computers on your network that are on 24/7, you can use them as a method of updating your network's IP address automatically. 

# How to Setup

You probably created a Device for your router, and configured the Legacy IPv4 resolvers on it. Let's assume it's called `my-router`. Simply copy the DNS-over-HTTPS resolver from the same Device, and configure it in a [Browser](doc:browsers-platform) of your choice, ideally on a machine that's online 24/7, and has a bunch of browser tabs open. Once you do this, the browser you chose will disregard your router's DNS, and use the Control D Device's resolver directly. Since browsers emit DNS queries on their own, especially if you have several tabs open, as soon as your network's IP address changes, the very first DNS query emitted from your browser will automatically authorize your new IP. 

You can find a list of all authorized IPs [here](https://controld.com/dashboard/ips). 

> 📘 Not just browsers
>
> The above example suggests that you use a browser, but you don't have to. Any Internet connected device that supports Secure DNS (Android, iOS, MacOS, Windows 11) can do the same task.

## Different Devices

The above example assumes you're using the same Control D Device both on your router AND in the browser of a chosen Heartbeat Device. We suggest doing this, as it's the simplest option. If you wish to use 2 separate Control D Devices, you can still do this but with a few extra steps. 

For the purposes of this example we're going to assume the following 2 Devices that you created:

* `my-router` -> setup on your router using Legacy DNS
* `my-chrome-browser` -> setup in Google Chrome on some machine on your network using DNS-over-HTTPS.

In the `my-chrome-browser` Device Settings, enable the [Expose IP via DNS](doc:expose-ip-via-dns) feature. When your browser makes DNS queries, the last seen source IP will be exposed via this DNS record, in a similar fashion to standard DDNS services. 

<Image title="expose-ip-1.JPG" alt={3736} align="center" src="https://files.readme.io/4300864-expose-ip-1.JPG">
  secret-browser-ip.controld.live is your (example) personal DDNS record.
</Image>

Then go into the `my-router` Device Settings, and configure the hostname you saw above as a  Dynamic DNS hostname. 

![](https://files.readme.io/bcdf4b4-expose-ip-2.JPG "expose-ip-2.JPG")

Once you do the above, the following things will happen.

1. Your browser makes random DNS requests, and updates the example `secret-browser-ip.controld.live` DNS record automatically. 
2. Your router's Device has DDNS enabled, using the above record. When it changes, Control D will auto-learn the new IP on the `my-router` Device, making Legacy DNS work.
