---
title: ctrld Known Issues
excerpt: Known ctrld issues, platform notes, and current workarounds.
hidden: false
metadata:
  robots: index
---
This page tracks known `ctrld` issues and current workarounds in one place. If you are trying to collect logs for support, see [How to Debug ctrld](doc:how-to-debug-ctrld).

# macOS

## Self-upgrade may fail on Darwin 15.5

**Status:** Under investigation
**Affected versions:** `ctrld` v1.4.2 and newer on macOS Darwin 15.5

On macOS Darwin 15.5, `ctrld` may attempt to self-upgrade but remain on the existing version.

**Workarounds:**

1. Upgrade macOS to Darwin 15.6 or newer, where `ctrld` self-upgrade has been tested successfully.
2. Manually run the upgrade command:

```bash
ctrld upgrade prod
```

# ASUSWRT-Merlin

## `ctrld` stops after pressing `Ctrl+C` in `ctrld log tail`

**Status:** Workaround available

On ASUSWRT-Merlin routers, `ctrld` can stop unexpectedly if the daemon and log viewer are run from the same SSH session, then `Ctrl+C` is used to stop `ctrld log tail`.

This can happen because both processes may share the same process group in that SSH session. Pressing `Ctrl+C` sends an interrupt signal to the foreground process group, which can also reach the attached `ctrld` daemon.

**Example trigger:**

1. Start the daemon manually:

```bash
ctrld start --cd=<resolver_id>
```

2. Tail logs in the same terminal:

```bash
ctrld log tail
```

3. Press `Ctrl+C` to stop viewing logs.

**Workaround:** Use separate SSH sessions:

- **Session A:** Start `ctrld` and leave it running.
- **Session B:** Run `ctrld log tail`.

Stopping log tail in Session B should not interrupt the daemon running in Session A.

# ASUS RT-AC68U

## `linux_armv7` binary does not run

**Status:** Workaround available

The ASUS RT-AC68U uses ARMv7 hardware, but the `linux_armv7` `ctrld` binary may not run on this router.

**Workaround:** Use the `linux_armv5` binary instead.

# UniFi Dream Machine / UDM Pro

## Static DHCP DNS settings bypass `ctrld`

**Status:** Configuration issue

On UDM devices, setting static external DNS servers under the DHCP **DNS Server** settings can cause LAN client DNS requests to bypass the local `ctrld` listener.

**Workaround:** Set the DHCP **DNS Server** option to **Auto** so LAN clients receive the correct DNS configuration.

## Policy-Based Routing can bypass `ctrld`

**Status:** Configuration limitation

When Policy-Based Routing is configured on a UDM network, firewall rules may redirect DNS requests to the WAN-side `dnsmasq` instance instead of the `ctrld` listener. This prevents client DNS requests from being handled by `ctrld`.

**Workaround:** DNS traffic must be routed to the `ctrld` listener with higher-priority firewall rules.

> 🚧 Advanced configuration
>
> Directly modifying UDM firewall or system configuration outside of the UniFi web interface is risky and is not officially supported. Incorrect changes can break connectivity or cause system instability.

# Windows

## VPN `block-outside-dns` breaks DNS in DNS intercept mode

**Status:** Fixed in `ctrld` v1.5.1
**Affected versions:** `ctrld` v1.5.0 and older when using DNS intercept mode on Windows

Some VPN clients use OpenVPN's `block-outside-dns` directive to install Windows Filtering Platform block rules. Those rules can block DNS traffic to non-tunnel interfaces, including the loopback listener at `127.0.0.1`.

When `ctrld` uses an NRPT catch-all rule to send DNS through the Windows DNS Client to `127.0.0.1:53`, those VPN block rules can prevent the DNS Client from reaching `ctrld`, causing DNS queries to time out.

This can affect VPN clients that implement `block-outside-dns` through Windows Filtering Platform, including:

- OpenVPN GUI
- Securepoint SSL VPN
- Other OpenVPN-based clients that honor the `block-outside-dns` push directive

**Fix:** Upgrade to `ctrld` v1.5.1 or newer. Newer versions add Windows Filtering Platform permit rules for DNS to localhost at startup so the NRPT-to-loopback path remains available while the VPN is connected.

# Report a new issue

If you run into an issue that is not listed here:

1. Check the [`ctrld` GitHub issues](https://github.com/Control-D-Inc/ctrld/issues) to see if it has already been reported.
2. If it has not been reported, open a new issue and include:
   - What happened
   - Steps to reproduce it
   - What you expected to happen
   - Operating system, version, and architecture
   - `ctrld` version
   - Relevant logs from [How to Debug ctrld](doc:how-to-debug-ctrld)

# Status legend

- **Under investigation:** The issue is confirmed or suspected and is still being analyzed.
- **Workaround available:** A temporary solution exists while the underlying issue remains open.
- **Configuration issue:** The behavior is caused by local device or network configuration.
- **Configuration limitation:** The device or platform can work, but it may need advanced configuration outside the normal setup path.
- **Fixed:** The issue was resolved in a specific `ctrld` version.
