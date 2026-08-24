---
title: ctrld Local Config Mode vs CD Mode
excerpt: >-
  Understand when ctrld uses Control D API-managed configuration and when it
  uses a local TOML file.
hidden: false
metadata:
  robots: index
---
`ctrld` can run in two broad configuration modes:

- **CD Mode**: `ctrld` is linked to a Control D Endpoint/Resolver ID and fetches its running configuration from the Control D API.
- **Local Config Mode**: `ctrld` runs from a local TOML config file that you edit and maintain yourself.

Most Control D users should use **CD Mode**. If you need advanced routing or custom upstreams while staying centrally managed, use the dashboard [Managed Custom ctrld TOML Config](doc:managed-custom-ctrld-toml-config) path. Use **Local Config Mode** only when you want the local TOML file itself to be the source of truth.

# Quick comparison

| Behavior | CD Mode | Local Config Mode |
| --- | --- | --- |
| How it starts | `ctrld start --cd RESOLVER_ID` or the Control D one-line installer | `ctrld start --config=/path/to/ctrld.toml` |
| Source of truth | Control D Endpoint configuration from the dashboard/API | Local `ctrld.toml` file |
| API connectivity | Required at startup and periodically while running | Not required for config updates |
| Config file on disk | Auto-generated from the Control D API | Manually edited by you |
| Dashboard changes | Applied after `ctrld` fetches updated API config | Not applied automatically |
| Manual edits to generated file | Overwritten | Preserved |
| `ctrld` self-upgrade target | Can be delivered through API-managed endpoint config | Must be handled manually |
| Best for | Normal Endpoint installs, dashboard-managed policy, and dashboard-managed custom TOML | Advanced routers, fully self-managed local files, or configs intentionally disconnected from dashboard changes |

# CD Mode

CD Mode is the default mode used by the Control D one-line installer and by commands that include `--cd RESOLVER_ID`.

Example:

```bash
sudo ctrld start --cd RESOLVER_ID
```

On Windows, run from an elevated Command Prompt or PowerShell:

```cmd
ctrld.exe start --cd RESOLVER_ID
```

In this mode, `ctrld`:

1. Contacts the Control D API (`api.controld.com`) using the Resolver ID.
2. Fetches the Endpoint's resolver configuration.
3. Generates a local `ctrld.toml` file from that API response.
4. Starts the `ctrld` service.
5. Configures the system or selected network interface to use the local `ctrld` listener.
6. Periodically checks the API for relevant updates while running.

The generated config file usually starts with this warning:

```text
# AUTO-GENERATED VIA CD FLAG - DO NOT MODIFY
```

That warning matters. In CD Mode, the local config file is an output of the Control D API state, not the source of truth. If you edit that generated file directly, your changes can be overwritten the next time `ctrld` starts or re-renders its configuration from the API.


# Managed custom TOML in CD Mode

CD Mode can still support advanced custom TOML when the config is saved through the Control D dashboard TOML Config editor. In that case, Control D remains the source of truth and `ctrld` fetches the managed custom config from the API.

Use [Managed Custom ctrld TOML Config](doc:managed-custom-ctrld-toml-config) when you need custom upstreams or split DNS on centrally managed endpoints, such as MDM/RMM-managed roaming clients.

# Local Config Mode

Local Config Mode means `ctrld` reads and enforces a TOML file from disk.

Example:

```bash
sudo ctrld start --config=/path/to/ctrld.toml
```

In this mode, `ctrld`:

1. Reads the config file you provide.
2. Starts its listener(s) from that file.
3. Uses the upstreams and routing policies defined in that file.
4. Preserves your local edits.

Dashboard-side Endpoint changes do not automatically rewrite this local file. If you change DNS policies in the Control D dashboard, those changes are not automatically reflected in your local TOML config unless you manually edit the file or switch back to CD Mode.

# Switching from CD Mode to Local Config Mode

If you installed `ctrld` with the Control D one-line installer or started it with `--cd`, and you now want to manage the TOML file yourself:

1. Stop the running service:

```bash
sudo ctrld stop
```

2. Copy the generated config to a file you intend to manage. Common paths are:

- Linux/macOS/FreeBSD: `/etc/controld/ctrld.toml`
- Windows: `C:\ControlD\ctrld.toml`

3. Remove the auto-generated warning from your working copy if present:

```text
# AUTO-GENERATED VIA CD FLAG - DO NOT MODIFY
```

4. Edit the TOML file for your desired listeners, upstreams, and routing policy.

5. Start `ctrld` with the explicit config file path:

```bash
sudo ctrld start --config=/path/to/ctrld.toml
```

After that, restart `ctrld` whenever you want it to apply local file changes:

```bash
sudo ctrld restart
```

# Running without automatic DNS steering

Sometimes you want `ctrld` to run as a service and listen on a port, but you do **not** want it to change system or interface DNS settings. For example, you may want `dnsmasq`, Windows DNS Server, or router firmware to forward queries to `ctrld` manually.

Use `service start` for that pattern.

CD Mode without automatic DNS steering:

```bash
sudo ctrld service start --cd=RESOLVER_ID
```

Local Config Mode without automatic DNS steering:

```bash
sudo ctrld service start --config=/path/to/ctrld.toml
```

In both cases, `ctrld` starts the service and listener(s), but DNS traffic must be pointed at those listener(s) by your own router, DNS server, or OS configuration.

# Common failure mode: editing the wrong source of truth

If you edit `ctrld.toml` but your changes disappear or do not take effect, check which mode you are actually running.

You are probably still in CD Mode if:

- The config file says `AUTO-GENERATED VIA CD FLAG - DO NOT MODIFY`.
- The service was installed with the Control D one-line installer.
- The service command includes `--cd` or was last started with `--cd`.
- Dashboard changes continue to affect the service.

You are probably in Local Config Mode if:

- The service command uses `--config=/path/to/ctrld.toml` without `--cd`.
- Your TOML edits persist across restarts.
- Dashboard-side Endpoint changes do not change the local config automatically.

# Which mode should I use?

Use **CD Mode** if you want:

- Normal Control D Endpoint onboarding.
- Dashboard-managed policy and settings.
- API-delivered updates to the Endpoint's `ctrld` configuration.
- The simplest support path.

Use **Local Config Mode** if you need:

- A local TOML file to be authoritative instead of Control D API state.
- Custom configs that should be edited only on the device/router.
- Source IP, subnet, hostname, or MAC-based routing policies that you do not want to manage through the dashboard TOML editor.
- A router or DNS server to steer traffic into `ctrld` manually.
- A fully self-managed local config file.

# Before contacting support

If you are troubleshooting a config issue, include:

- Which mode you intended to use: CD Mode or Local Config Mode.
- The exact command used to start `ctrld`.
- Whether the config file contains `AUTO-GENERATED VIA CD FLAG - DO NOT MODIFY`.
- The operating system or router firmware.
- Debug logs from [How to Debug ctrld](doc:how-to-debug-ctrld).

Do not include API tokens, private keys, or other secrets from your config file.
