---
title: Free DNS Resolvers
excerpt: Free community DNS resolvers you can use without an account.
deprecated: false
hidden: false
metadata:
  robots: index
---
### TL;DR

Control D offers **free, public DNS resolver endpoints** you can use without needing an account. They let you resolve domain names with built-in filtering (optional) and encryption, backed by our global anycast network.

***

## Why We Offer Them

* To let anyone benefit from faster, safer DNS without signing up
* To showcase our filtering in “open mode”
* To help folks who don’t want the overhead of managing a full account or dashboard
* To let devs / power users test configurations easily

***

## What They Do / Don’t Do

### What They _Do_

* Resolve DNS queries (map domain names to IPs)
* Support encrypted DNS (DoH, DoT, QUIC)
* Optionally block domains according to curated Native and 3rd-party blocklists (ads, malware, tracking, etc.)
* Refresh those blocklists periodically (every 30 minutes) so filters stay current
* Operate over an anycast infrastructure to reduce latency and improve reliability
* Not store logs (no individual browsing history, timestamps, or query logs)

### What They _Don’t_ Do

* They are **not** a full dashboard / profile management system
* You cannot create custom rules or fine-tune individual domains (beyond what the blocklists provide)
* They don’t provide analytics or reporting
* If you want custom Filters or per-device profiles, that’s in the paid offering

***

## How They’re Structured

We expose multiple blocklist presets as distinct resolver endpoints. Each flavor corresponds to one or more blocklists. You pick whichever fits your needs:

## Native Filters

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Name
      </th>

      <th>
        Legacy DNS
      </th>

      <th>
        Secure DNS (DNS-over-HTTPS/TLS/QUIC)
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Unfiltered
      </td>

      <td>
        `76.76.2.0`  
        `76.76.10.0`  
        `2606:1a40::0`  
        `2606:1a40:1::0`
      </td>

      <td>
        * `https://freedns.controld.com/p0`
        * `p0.freedns.controld.com`
        * `quic://p0.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        Malware
      </td>

      <td>
        `76.76.2.1`  
        `76.76.10.1`  
        `2606:1a40::1`  
        `2606:1a40:1::1`
      </td>

      <td>
        * `https://freedns.controld.com/p1`
        * `p1.freedns.controld.com`
        * `quic://p1.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        Ads & Tracking
      </td>

      <td>
        `76.76.2.2`  
        `76.76.10.2`  
        `2606:1a40::2`  
        `2606:1a40:1::2`
      </td>

      <td>
        * `https://freedns.controld.com/p2`
        * `p2.freedns.controld.com`
        * `quic://p2.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        Social
      </td>

      <td>
        `76.76.2.3`  
        `76.76.10.3`  
        `2606:1a40::3`  
        `2606:1a40:1::3`
      </td>

      <td>
        * `https://freedns.controld.com/p3`
        * `p3.freedns.controld.com`
        * `quic://p3.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        Family Friendly
      </td>

      <td>
        `76.76.2.4`  
        `76.76.10.4`  
        `2606:1a40::4`  
        `2606:1a40:1::4`
      </td>

      <td>
        * `https://freedns.controld.com/family`
        * `family.freedns.controld.com`
        * `quic://family.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        Uncensored
      </td>

      <td>
        `76.76.2.5`  
        `76.76.10.5`  
        `2606:1a40::5`  
        `2606:1a40:1::5`
      </td>

      <td>
        * `https://freedns.controld.com/uncensored`
        * `uncensored.freedns.controld.com`
        * `quic://uncensored.freedns.controld.com`
      </td>
    </tr>
  </tbody>
</Table>

## 3rd-Party Filters

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Name
      </th>

      <th>
        Legacy DNS
      </th>

      <th>
        Secure DNS (DNS-over-HTTPS/TLS/QUIC)
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [OISD Full](https://oisd.nl/downloads)
      </td>

      <td>
        `76.76.2.32`  
        `76.76.10.32`  
        `2606:1a40::32`  
        `2606:1a40:1::32`
      </td>

      <td>
        * `https://freedns.controld.com/x-oisd`
        * `x-oisd.freedns.controld.com`
        * `quic://x-oisd.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [OISD Basic](https://oisd.nl/downloads)
      </td>

      <td>
        `76.76.2.33`  
        `76.76.10.33`  
        `2606:1a40::33`  
        `2606:1a40:1::33`
      </td>

      <td>
        * `https://freedns.controld.com/x-oisd-basic`
        * `x-oisd-basic.freedns.controld.com`
        * `quic://x-oisd-basic.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [StevenBlack Unified](https://github.com/StevenBlack/hosts)
      </td>

      <td>
        `76.76.2.35`  
        `76.76.10.35`  
        `2606:1a40::35`  
        `2606:1a40:1::35`
      </td>

      <td>
        * `https://freedns.controld.com/x-stevenblack`
        * `x-stevenblack.freedns.controld.com`
        * `quic://x-stevenblack.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [1Hosts Lite](https://github.com/badmojr/1Hosts)
      </td>

      <td>
        `76.76.2.38`  
        `76.76.10.38`  
        `2606:1a40::38`  
        `2606:1a40:1::38`
      </td>

      <td>
        * `https://freedns.controld.com/x-1hosts-lite`
        * `x-1hosts-lite.freedns.controld.com`
        * `quic://x-1hosts-lite.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [1Hosts Pro](https://github.com/badmojr/1Hosts)
      </td>

      <td>
        `76.76.2.39`  
        `76.76.10.39`  
        `2606:1a40::39`  
        `2606:1a40:1::39`
      </td>

      <td>
        * `https://freedns.controld.com/x-1hosts-pro`
        * `x-1hosts-pro.freedns.controld.com`
        * `quic://x-1hosts-pro.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [1Hosts Xtra](https://github.com/badmojr/1Hosts)
      </td>

      <td>
        `76.76.2.48`  
        `76.76.10.48`  
        `2606:1a40::48`  
        `2606:1a40:1::48`
      </td>

      <td>
        * `https://freedns.controld.com/x-1hosts-xtra`
        * `x-1hosts-xtra.freedns.controld.com`
        * `quic://x-1hosts-xtra.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [Hagezi's DNS Light](https://github.com/hagezi/dns-blocklists)
      </td>

      <td>
        `76.76.2.37`  
        `76.76.10.37`  
        `2606:1a40::37`  
        `2606:1a40:1::37`
      </td>

      <td>
        * `https://freedns.controld.com/x-hagezi-light`
        * `x-hagezi-light.freedns.controld.com`
        * `quic://x-hagezi-light.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [Hagezi's DNS Normal](https://github.com/hagezi/dns-blocklists)
      </td>

      <td>
        `76.76.2.40`  
        `76.76.10.40`  
        `2606:1a40::40`  
        `2606:1a40:1::40`
      </td>

      <td>
        * `https://freedns.controld.com/x-hagezi-normal`
        * `x-hagezi-normal.freedns.controld.com`
        * `quic://x-hagezi-normal.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [Hagezi's DNS Pro](https://github.com/hagezi/dns-blocklists)
      </td>

      <td>
        `76.76.2.41`  
        `76.76.10.41`  
        `2606:1a40::41`  
        `2606:1a40:1::41`
      </td>

      <td>
        * `https://freedns.controld.com/x-hagezi-pro`
        * `x-hagezi-pro.freedns.controld.com`
        * `quic://x-hagezi-pro.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [Hagezi's DNS Pro Plus](https://github.com/hagezi/dns-blocklists)
      </td>

      <td>
        `76.76.2.42`  
        `76.76.10.42`  
        `2606:1a40::42`  
        `2606:1a40:1::42`
      </td>

      <td>
        * `https://freedns.controld.com/x-hagezi-proplus`
        * `x-hagezi-proplus.freedns.controld.com`
        * `quic://x-hagezi-proplus.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [Hagezi's DNS Ultimate](https://github.com/hagezi/dns-blocklists)
      </td>

      <td>
        `76.76.2.45`  
        `76.76.10.45`  
        `2606:1a40::45`  
        `2606:1a40:1::45`
      </td>

      <td>
        * `https://freedns.controld.com/x-hagezi-ultimate`
        * `x-hagezi-ultimate.freedns.controld.com`
        * `quic://x-hagezi-ultimate.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [Hagezi's DNS TIF](https://github.com/hagezi/dns-blocklists)
      </td>

      <td>
        `76.76.2.46`  
        `76.76.10.46`  
        `2606:1a40::46`  
        `2606:1a40:1::46`
      </td>

      <td>
        * `https://freedns.controld.com/x-hagezi-tif`  
          -`x-hagezi-tif.freedns.controld.com`  
          -`quic://x-hagezi-tif.freedns.controld.com`
      </td>
    </tr>

    <tr>
      <td>
        [AdGuard Filter](https://github.com/AdguardTeam/AdGuardSDNSFilter)
      </td>

      <td>
        `76.76.2.44`  
        `76.76.10.44`  
        `2606:1a40::44`  
        `2606:1a40:1::44`
      </td>

      <td>
        * `https://freedns.controld.com/x-adguard`
        * `x-adguard.freedns.controld.com`
        * `quic://x-adguard.freedns.controld.com`
      </td>
    </tr>

  </tbody>
</Table>

# Update Interval

All Filters are rebuilt and deployed from their original sources every 30 minutes.

***

## Setup & Endpoints

You point your device, router, or app to one of the free DNS endpoints:

* For **legacy DNS**: use the IPv4 or IPv6 addresses listed above
* For **secure DNS (DoH / DoT / QUIC)**: use the hostname / URL (e.g. `x-oisd.freedns.controld.com`)

Because these resolvers are global (anycast), your queries will be routed to the nearest healthy node automatically.

***

## Limitations & Things to Watch Out For

* You can’t “mix & match” filters (e.g. use StevenBlack _plus_ some custom domain)
* Some 3rd-party blocklists may be overzealous or block false positives
* Devices relying on captive portals (e.g. hotel Wi-Fi) may fail DNS until portal is accepted
* If you ever migrate to full Control D, you’ll need to switch DNS endpoints
* Free resolvers do **not** include logging or historical query data
