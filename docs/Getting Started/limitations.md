---
title: Limitations
excerpt: Here are things you cannot/should not do with Control D.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
Control D is not magic, it will not solve wealth disparity or world hunger, and it will also **not help you** with any of the following. 

# 🚫 Block BitTorrent Protocol

Control D can block Torrent search engines and trackers using the Torrents filter. This can make it much more difficult for someone on your network to use the BitTorrent  protocol, but it will not actually prevent it from working, since it does not use DNS. A protocol-aware firewall is your best option. 

# 🚫 Life-critical Anonymity

If you live in a country where freedom of speech is non-existent, or if you are a whistleblower, dissident or political activist, you should not use Control D to stay safe online.

Despite Control D encrypting your DNS queries (if you use Secure DNS protocols), even if you are using the proxy capabilities to spoof your location, the Server Name Indication (SNI) TLS extension is still transmitted in plaintext. This means that on adversarial networks where this information is captured and filtered, Control D will not provide you any security benefits. It will not be able to unblock restricted sites, and your browsing history could still be captured by the network administrator. You should use a VPN.

# 🚫 Not a VPN

This goes without saying, but Control D is not a Virtual Private Network (VPN) provider. Control D is a DNS service, that can redirect all your HTTP (and some non-SNI enabled) traffic through a series of transparent proxies in over 100 city level locations, so the sites you visit will not see your IP address, but that of one of our proxies, courtesy of [Windscribe](https://windscribe.com) (our sister company). Your network administrator or ISP will not see the contents of your DNS queries if you use a secure DoH or DoT resolver, however those deploying DPI technologies could still determine the sites you visit by looking at SNI information which is currently not encrypted.
