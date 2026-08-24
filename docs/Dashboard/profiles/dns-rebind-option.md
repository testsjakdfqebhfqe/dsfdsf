---
title: DNS Rebind Protection
excerpt: Blocks domains that point to private IP addresses.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This is a Profile Option that you can enable on any of your Profiles. With this enabled, any Endpoint that enforces this Profile will not resolve any RFC1918 and loopback (localhost) addresses found in public DNS. You can still make your own Custom Rules that spoof domains to to these IP ranges.

# Example

No DNS rebind protection.

```
test@test-vm:~$ dig +short rfc1918.test.controld.org
192.168.0.1
```

Now enable DNS rebind protection.

```
test@test-vm:~$ dig +short rfc1918.test.controld.org
0.0.0.0
```

## Addresses included in DNS Rebind Protection

| Address           | Description                                        |
| ----------------- | -------------------------------------------------- |
| 127.0.0.0/8       | RFC 1122 Loopback Addresses (Localhost)            |
| 10.0.0.0/8        | RFC 1918 Private Addresses                         |
| ::ffff:a00:0/104  | IPv6 Representation of 10.0.0.0/8                  |
| 172.16.0.0/12     | RFC 1918 Private Addresses                         |
| ::ffff:ac10:0/108 | IPv6 Representation of 172.16.0.0/12               |
| 192.168.0.0/16    | RFC 1918 Private Addresses                         |
| ::ffff:c0a8:0/112 | IPv6 Representation of 192.168.0.0/16              |
| 169.254.0.0/16    | RFC 3927 IPv4 Link Local Addresses                 |
| ::ffff:a9fe:0/112 | IPv6 Representation of 169.254.0.0/16              |
| fd00::/8          | RFC 4193 IPv6 Unique Local Unicast Addresses (ULA) |
| fe80::/10         | RFC 4291 IPv6 Link Local Addresses                 |
