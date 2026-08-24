---
title: macOS MDM Deployment (.pkg)
excerpt: >-
  Deploy ctrld to macOS fleets through your MDM using a signed .pkg and a
  configuration profile.
hidden: false
metadata:
  description: >-
    Deploy the Control D daemon (ctrld) to macOS fleets with Jamf, Intune,
    Mosyle or any MDM using a signed installer package and a configuration
    profile.
  keywords:
    - mdm
    - jamf
    - intune
    - mosyle
    - pkg
    - macos
    - mass provisioning
  robots: index
---
> 🚧 Organizations Only
>
> An Organization account is required to use this feature.

# Overview

The macOS installer package deploys `ctrld` to managed fleets through Jamf, Intune, Mosyle, or any MDM that installs signed packages. It is a single generic package per release: provisioning credentials are delivered separately through a configuration profile, never inside the package.

Requirements: macOS 12 (Monterey) or later, Intel or Apple Silicon (the package is universal). The package is signed with a Developer ID Installer certificate, notarized and stapled, so it installs on machines without internet access to Apple.

# How it works

1. Your MDM installs a configuration profile that delivers the provisioning token to the `com.controld.ctrld` managed preferences domain.
2. Your MDM installs the package. Its install script reads the token and enrolls the device: the token is exchanged once for a per-device Endpoint, and the token itself is discarded.
3. Later package installs are upgrades: the binary is replaced and the service restarted. Endpoint identity and configuration are untouched, and upgrades keep working even after the provisioning code is revoked.

# Step 1: Create a provisioning code

Follow [Mass Provisioning](/docs/provisioning) to create a provisioning code with Endpoint Type **Mac**. The code's Expires After and Limit settings control enrollment, and revoking the code stops new enrollments without affecting enrolled devices.

# Step 2: Download the deployment artifacts

Open **Provisioning Instructions** on the code. Under the MDM section:

- **Download Configuration Profile** — a `.mobileconfig` pre-filled with this code's token.
- **Download .pkg Installer** — the current signed universal package.

Jamf Pro admins can alternatively use Computers → Configuration Profiles → Application & Custom Settings → External Applications with preference domain `com.controld.ctrld` and this schema, entering the provisioning token in the rendered form:

```json
{
    "title": "Control D (ctrld)",
    "description": "Provisioning settings for the ctrld macOS package.",
    "properties": {
        "ProvisionToken": {
            "title": "Provision Token",
            "description": "Token from the Control D mass-provisioning code. Required: fresh installs read it at package install time to enroll the device.",
            "type": "string"
        },
        "CustomHostname": {
            "title": "Custom Hostname",
            "description": "Optional hostname reported to the Control D API instead of the device hostname.",
            "type": "string"
        }
    }
}
```

# Step 3: Deploy

1. Upload the configuration profile to your MDM as a **device (System) profile** and scope it to the fleet.
2. Upload the package and scope it to the same fleet.

**Scope the profile before the package.** The install script waits up to 2 minutes for the profile; if it never arrives, the install is reported as **failed** in the MDM and the service does not start (see Troubleshooting).

Installation is unattended: no user interaction, no reboot. On install each device enrolls and appears as an Endpoint in the Control D dashboard. To verify on a device:

```shell
sudo /usr/local/bin/ctrld status
pkgutil --pkg-info com.controld.ctrld
```

# Upgrades

Push a newer package version through the MDM. The installer stops the service, replaces the binary, and restarts the service. The Endpoint, its configuration, and the dashboard entry are preserved. No provisioning token is needed for upgrades.

Note: `ctrld upgrade` (the built-in self-updater) also works on package-based installs. MDM-managed fleets should standardize on package pushes so the package receipt version reflects reality; avoid scheduling `ctrld upgrade` on managed devices.

# Offboarding

Run the bundled uninstall helper from an MDM script or policy, as root:

```shell
/usr/local/controld/uninstall.sh [deactivation-pin]
```

If the provisioning code was created with a Prevent Deactivation PIN, pass it as the first argument — store it as a server-side script parameter in the MDM (for example a Jamf script parameter), never in a script visible to users. The helper stops the service, restores DNS to OS defaults, and removes the configuration, binary, and package receipt.

The corresponding Endpoint can then be removed in the Control D dashboard. Endpoints (and their analytics) remain in the dashboard until removed — an uninstalled device simply stops reporting. Removing the Endpoint first also works, but only partially: on its next service start ctrld detects the missing Endpoint, stops itself, and restores the device's normal DNS — but the binary, launchd service, and package receipt stay on disk. Run the uninstall helper (or push an MDM removal) to fully remove ctrld.

# Troubleshooting

Install script output lands in `/var/log/install.log` on the device, prefixed `ctrld postinstall:` / `ctrld preinstall:`. The provisioning token is never written to logs.

A **failed install in the MDM** means the device did not end up with a running provisioned service. The files stay on disk (macOS Installer does not roll back), so remediation is always: fix the cause, then re-push the package.

- **"no ProvisionToken in managed preferences"** — the profile was not scoped, or arrived late. Scope the profile, confirm with `sudo defaults read "/Library/Managed Preferences/com.controld.ctrld"`, then re-push the package.
- **"provisioning did not complete"** — token invalid, expired, at its enrollment limit, or no network. Check the provisioning code in the dashboard, then re-push the package.
- **"upgrade installed but service failed to reload"** — the new binary is in place but the service did not restart; run `sudo launchctl load /Library/LaunchDaemons/ctrld.plist` or re-push the package.
