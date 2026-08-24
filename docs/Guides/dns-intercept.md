---
title: DNS Intercept Mode
excerpt: Stop VPN software from fighting with Control D over DNS settings.
deprecated: false
hidden: false
metadata:
  robots: index
---
When you use Control D alongside VPN software, there can be unexpected behaviour such as:

* **Intermittent failures** — DNS randomly stops working for a few seconds
* **Bypassed filtering** — Queries sneak through to the VPN's DNS, skipping your Control D profile
* **Infinite loops** — Control D sets DNS, VPN overwrites it, Control D fixes it, VPN overwrites again...

## When to Use This

Enable DNS Intercept Mode if you:

* Use corporate VPN software (F5, Cisco, Palo Alto, Zscaler)
* Run Tailscale, WireGuard, or other overlay networks
* Experience random DNS failures when VPN connects/disconnects
* See gaps in your Control D analytics when VPN is active
* Have endpoint security software that also manages DNS

## How to Enable

Add `--intercept-mode` to your ctrld start command:

```bash
ctrld start --intercept-mode dns --cd RESOLVER_ID_HERE
```

`--intercept-mode dns` automatically detects VPN internal domains and routes them correctly while Control D handles everything else.

`--intercept-mode off` will disable this feature and restore the default behavior of Control D.

## Platform Support

| Platform | Supported | How It Works                                                                 |
| -------- | --------- | ---------------------------------------------------------------------------- |
| Windows  | ✅         | Uses NRPT (Name Resolution Policy Table)                                     |
| macOS    | ✅         | Uses pf (packet filter) to redirect DNS traffic                              |
| Linux    | ❌         | Not currently supported (Linux DNS stacks don't have the same VPN conflicts) |

## Additional Features

* **Captive portal recovery** — Wi-Fi login pages (hotels, airports, coffee shops) work automatically
* **No network adapter changes** — Your DNS settings stay untouched, eliminating conflicts entirely

## Known VPN Compatibility

DNS Intercept Mode has been tested with:

* ✅ F5 BIG-IP APM
* ✅ Cisco AnyConnect
* ✅ Palo Alto GlobalProtect
* ✅ Tailscale (including Exit Nodes)
* ✅ Windscribe
* ✅ WireGuard
