---
title: High latency/slow speeds
excerpt: Seeing performance issues? Collect some data and send it our way.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Control D operates on top of an anycast network, so your traffic should be routed to the [closest server location](https://controld.com/network/) under normal circumstances. However, nothing is perfect, so in order for us to troubleshoot performance issues, we need the following:

1. Results from [the Status page](https://controld.com/status) (use the purple Copy Results button)
2. Traceroute (instructions below)
3. Take the data and email it to [help@controld.com](mailto:help@controld.com), along with:
   1. Network Type [Residential / Work / School / Other (please specify)]\:
   2. Network Architecture [Fiber / Cable / DSL / Wireless Broadband (5G-powered "Airfiber" falls under this category) / Cellular / Satellite / Other (please specify)]\:
   3. Brief overview of issue
   4. Is there different behavior at different times of day? Please provide a traceroute from both times if so

# Status Page

On the device that is experiencing the issue, navigate to the [Status Page](https://controld.com/status/) ([https://controld.com/status](https://controld.com/status)), and press the "Copy Results" button. It will look something like this (when you paste it)

```
    Control D Troubleshooting - Thu, 26 Jan 2023 16:48:23 UTC
    -------------------------------------------------------------------
    IPv4 Address      |  66.207.xxx.xxx (Beanfield Technologies)
    IPv6 Address      |  2607:f0c8:8000:8210:xxx:xxx:xxx:xxx
    Using Control D   |  YYZ
    Resolver          |  REDACTED
    DNS Protocol      |  DNS-over-HTTPS
    DNS Latency       |  0.93ms
    DNS Host          |  yyz-h02
    DNS Source IP     |  2607:f0c8:8000:8210:xxx:xxx:xxx:xxx
    Proxy Authorized  |  Yes
    Null Routed       |  No
    Proxy Latency     |  0.61ms
    Proxy Host        |  yyz-h02
    Proxy Source IP   |  2607:f0c8:8000:8210:xxx:xxx:xxx:xxx
```

## If Status Page Not Available

If you're unable to load the status page, collect data manually from these endpoints:

* [https://api.controld.com/ip/nullroutecheck](https://api.controld.com/ip/nullroutecheck)
* [https://dns.controld.com/info](https://dns.controld.com/info)
* [https://proxy-latency.controld.com:42069/info](https://proxy-latency.controld.com:42069/info)

# Traceroute

Please copy and paste the results of the traceroutes rather than sending a screenshot for faster resolution.

* For DNS related troubleshooting, trace: `dns.controld.com`
* For proxy related troubleshooting: trace: `proxy-latency.controld.com`

## Windows

Go to Start, search for “cmd” and open the Command Prompt. Enter this command: ` tracert dns.controld.com` (or the other hostname)

You should see something like this:

```
C:\>tracert dns.controld.com
Tracing route to controld.com [76.76.10.1]
over a maximum of 30 hops:
  1     1 ms    <1 ms     1 ms  REDACTED
  2    <1 ms    <1 ms    <1 ms  hu0-0-1-0.pe26.151FrontStW01.YYZ.beanfield.com [199.167.152.120]
  3    19 ms    15 ms    20 ms  76-9-214-10.beanfield.net [76.9.214.10]
  4    <1 ms    <1 ms    <1 ms  dns,controld.com [76.76.10.1]
Trace complete.
```

## Mac

Open Terminal. Enter this command: `traceroute dns.controld.com` (or the other hostname)

You should see something like this:

```
iMac:~ user$ traceroute dns.controld.com
traceroute to controld.com (76.76.10.1), 64 hops max, 52 byte packets
 1  REDACTED
 2  REDACTED
 3  hu0-0-1-0.pe25.151frontstw01.yyz.beanfield.com (199.167.152.86)  1.107 ms  1.141 ms  0.907 ms
 4  hu0-0-1-0.pe26.151frontstw01.yyz.beanfield.com (199.167.152.120)  1.126 ms  1.103 ms  1.041 ms
 5  76-9-214-10.beanfield.net (76.9.214.10)  20.661 ms  16.811 ms  18.972 ms
 6  dns.controld.com (76.76.10.1)  0.557 ms  0.456 ms  0.420 ms
```

To perform an IPv6 traceroute, use `traceroute6 dns.controld.com`

## Linux

Open Terminal. Enter this command: `sudo mtr -w -z --show-ips --report-cycles=10 dns.controld.com` 

You should see something like this:

```
user@ubuntu:/$ sudo mtr -w -z --show-ips --report-cycles=10 dns.controld.com
Start: 2021-05-05T14:35:09-0400
HOST: ubuntu                                                                     Loss%   Snt   Last   Avg  Best  Wrst StDev
  1. AS???    REDACTED                                                           0.0%    10    0.2   0.3   0.2   0.7   0.1
  2. AS21949  REDACTED                                                           0.0%    10    1.4   1.4   1.1   1.9   0.2
  3. AS21949  hu0-0-1-0.pe26.151FrontStW01.YYZ.beanfield.com (199.167.152.120)   0.0%    10    1.2   1.4   1.1   1.8   0.2
  4. AS21949  76-9-214-10.beanfield.net (76.9.214.10)                            0.0%    10   15.1  25.9   2.6 136.2  39.1
  5. AS398962 dns.controld.com (76.76.10.1)                                          0.0%    10    0.6   0.9   0.5   2.7   0.8
```

If you do not have MTR installed, use this command instead: `sudo traceroute -I dns.controld.com`

You should see something like this:

```
user@ubuntu:/$ sudo traceroute dns.controld.com
traceroute to controld.com (76.76.10.1), 30 hops max, 60 byte packets
 1  REDACTED
 2  REDACTED
 3  hu0-0-1-0.pe26.151FrontStW01.YYZ.beanfield.com (199.167.152.120)  1.188 ms  1.181 ms  1.137 ms
 4  76-9-214-10.beanfield.net (76.9.214.10)  18.181 ms  18.173 ms  18.166 ms
 5  dns.controld.com (76.76.10.1)  0.406 ms  0.340 ms  0.389 ms
```

Take the status page results + traceroute, and [email it to support](https://controld.com/contact/).
