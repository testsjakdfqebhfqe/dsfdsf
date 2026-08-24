---
title: Managed Custom ctrld TOML Config
excerpt: >-
  Manage advanced ctrld TOML configs from the Control D dashboard for
  cloud-managed endpoints.
hidden: false
metadata:
  robots: index
---
Use the dashboard TOML Config editor when you need advanced `ctrld` behavior on a Control D managed Endpoint, but you still want the Control D dashboard/API to remain the source of truth.

This is useful for cases such as:

- split-horizon DNS
- custom upstreams
- local resolvers such as `dnsmasq`
- custom listener or policy rules
- MDM/RMM-managed roaming clients where admins should not edit local files by hand

# How this differs from editing ctrld.toml locally

When `ctrld` is installed with the Control D one-line installer or started with `--cd RESOLVER_ID`, it runs in CD Mode. In CD Mode, the local `ctrld.toml` file is generated from Control D API state.

That generated file may contain this warning:

```text
# AUTO-GENERATED VIA CD FLAG - DO NOT MODIFY
```

Do not treat that generated file as the durable source of truth. Manual edits can be replaced when `ctrld` restarts or fetches updated managed configuration.

The dashboard TOML Config editor is the managed path for persistent custom TOML. You save the custom TOML in Control D, and the Endpoint receives it on its next managed config fetch.

For a deeper comparison, see [ctrld Local Config Mode vs CD Mode](doc:ctrld-local-config-vs-cd-mode).

> 📘 Important: This is a full ctrld config.

The TOML Config editor stores a complete custom `ctrld` config for that Endpoint. Treat it as the full desired `ctrld` configuration, not a small patch on top of the generated config.

If the Endpoint should continue sending normal DNS traffic to Control D, include the Control D upstream/default route explicitly in the custom TOML.

If you only define local split-DNS rules and omit the Control D upstream, normal DNS traffic may not use Control D as intended.

# Basic deployment flow

1. Open the relevant Endpoint/Device in the Control D dashboard.
2. Open the `ctrld` configuration modal.
3. Enter or update the TOML config in the TOML Config editor.
4. Save the config.
5. Restart `ctrld` on the target endpoint to force an immediate fetch, or wait for the next managed config fetch.
6. Confirm the dashboard shows the custom config as deployed after the endpoint fetches it.

Once fetched, the config is managed from the dashboard and persists across normal `ctrld` restarts/syncs. Do not make follow-up changes by editing the generated local `ctrld.toml` file.

# Example: route local development domains to dnsmasq

This example sends `.target` and `.internal` queries to a local `dnsmasq` instance, while all other DNS uses Control D.

```toml
[upstream.0]
  name = "Control D"
  type = "doh"
  endpoint = "https://dns.controld.com/YOUR_RESOLVER_ID"
  timeout = 5000

[upstream.1]
  name = "Local dnsmasq"
  type = "legacy"
  endpoint = "127.0.0.1:5354"
  timeout = 1000

[listener.0]
  ip = "127.0.0.1"
  port = 53

[listener.0.policy]
  rules = [
    {"target" = ["upstream.1"]},
    {"*.target" = ["upstream.1"]},
    {"internal" = ["upstream.1"]},
    {"*.internal" = ["upstream.1"]},
  ]
```

Replace `YOUR_RESOLVER_ID` with the Control D resolver endpoint shown for your Endpoint.

In this example:

- `target` / `*.target` queries go to local `dnsmasq`
- `internal` / `*.internal` queries go to local `dnsmasq`
- all other queries use the Control D upstream
- the custom config is saved in the dashboard, not manually edited on disk

# macOS dnsmasq port note

On macOS, port `5353` is commonly used by Apple's mDNS/Bonjour service. If your `dnsmasq` instance is already confirmed to be listening on `127.0.0.1:5353`, you can point `ctrld` at that address.

For fleet or MDM deployments, we recommend using a loopback-only non-mDNS port such as `127.0.0.1:5354` or `127.0.0.1:15353` where possible.

The `ctrld` listener port and the `dnsmasq` upstream port are separate:

- `ctrld` listens for system DNS on local port `53`
- `dnsmasq` listens on another local port, for example `127.0.0.1:5354`
- `ctrld` forwards only matching policy rules, such as `.target` and `.internal`, to `dnsmasq`

Do not configure `dnsmasq` to bind the same local DNS port that `ctrld` is using.

# Troubleshooting

## My local ctrld.toml edits disappear

The endpoint is probably running in CD Mode. Use the dashboard TOML Config editor for managed custom TOML, or switch to Local Config Mode if you want a local file to be the source of truth.

## The dashboard says the config is not deployed

The endpoint has not fetched the saved custom config yet. Restart `ctrld` on the endpoint to force a fetch, or wait for the next managed config fetch.

## Normal DNS stops using Control D

Check whether the custom TOML includes the Control D upstream/default route. The dashboard TOML Config editor stores a full config, so custom upstreams and the Control D upstream both need to be represented.

## Local split DNS does not resolve

Check that the local resolver is reachable from the endpoint:

- `dnsmasq` is running
- it is listening on the expected loopback IP and port
- local firewall/security software permits `ctrld` to query it
- the policy rules include both apex and wildcard forms where needed, such as `internal` and `*.internal`

# Before contacting support

Include:

- the Endpoint/Resolver ID
- the intended custom TOML, with secrets removed
- the operating system and deployment method, such as MDM/RMM
- whether the dashboard shows the custom config as deployed
- `ctrld` debug logs from [How to Debug ctrld](doc:how-to-debug-ctrld)

<br />
