---
title: Migrating from NextDNS to Control D
excerpt: >-
  Move from NextDNS to Control D by mapping profiles, filters, allow/block
  lists, rewrites, devices, and logs, then switching traffic in stages.
hidden: false
metadata:
  robots: index
---
Migrate from NextDNS to Control D by recreating your profiles, filtering settings, allow/block lists, rewrites, device deployments, and logging preferences, then testing with a small group before changing production DNS.

## Working Model

Most NextDNS migrations are a concept-mapping exercise:

1. For each NextDNS configuration ID/profile, create the equivalent Control D Profile.
2. Recreate broad security, privacy, content, and service controls with Control D Filters and Services.
3. Import explicit allow/deny entries as Control D Custom Rules.
4. Recreate DNS rewrites and local-domain behavior where needed.
5. Attach the Control D Profile to the right Control D Endpoint, then validate Activity Log results before switching everyone over.

If you currently rely on the NextDNS client or router agent, `ctrld` can also help with a staged migration. Its **NextDNS Mode** lets you run `ctrld` while still forwarding to a NextDNS profile first, so you can validate the daemon, router install, local listener, and client metadata behavior before switching the upstream to Control D.

## NextDNS to Control D: Concept Map

| NextDNS Concept                    | What It Means in NextDNS                                                                                                                                           | Control D Equivalent                                                                                                                                                              |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Configuration ID / Profile         | The NextDNS policy container that controls blocklists, security settings, privacy settings, parental controls, rewrites, allowlist, denylist, analytics, and logs. | Control D Profile. Profiles contain Filters, Services, Custom Rules, and Profile Options. A Profile only takes effect when enforced on an Endpoint.                               |
| Setup ID in DoH/DoT/DoQ URL        | The ID embedded in the resolver hostname or URL to bind DNS traffic to a NextDNS configuration.                                                                    | Control D resolver/Endpoint hostname, DoH URL, DoT hostname, DoQ endpoint, or `ctrld` provisioning command for the target Endpoint.                                               |
| Linked IP                          | A source IP authorized to use a NextDNS configuration over legacy DNS.                                                                                             | Control D Endpoint with source IP authorization or Dynamic DNS/heartbeat behavior, if legacy DNS is required. Prefer encrypted DNS or `ctrld` where possible.                     |
| Device name / device identifier    | Metadata used to separate logs and analytics for clients using the same NextDNS profile.                                                                           | Control D Endpoint naming, separate Endpoints, device clients, or `ctrld` client metadata depending on deployment shape.                                                          |
| Security settings                  | Native protection toggles such as threat, typo, or domain-generation protections.                                                                                  | Control D Filters. Enable the closest matching security Filters and review behavior before cutover.                                                                               |
| Privacy blocklists                 | Third-party or native lists used to block ads, trackers, and privacy-invasive domains.                                                                             | Control D Filters, including native and third-party options. Do not assume every list has a one-to-one equivalent; choose the closest list set and test.                          |
| Allowlist                          | Domains that should bypass filtering.                                                                                                                              | BYPASS Custom Rules. Custom Rules are evaluated before Services and Filters, making them the right place for exceptions.                                                          |
| Denylist                           | Domains that should always be blocked.                                                                                                                             | BLOCK Custom Rules, ideally grouped in a clearly named folder such as `NextDNS Block List - Profile Name`.                                                                        |
| Rewrites                           | Custom DNS answers for specific names, often used for local hosts or split-horizon behavior.                                                                       | REDIRECT Custom Rules for supported public targets, or local DNS / Active Directory / split-horizon handling for private/internal names. Review private records before migration. |
| Parental controls / service blocks | Category, app, or service-level blocking.                                                                                                                          | Control D Services and Filters. Use Services where a named app/service exists; otherwise use Custom Rules.                                                                        |
| Logs and analytics                 | Query visibility and retention settings.                                                                                                                           | Control D Activity Log and Analytics. Configure the Endpoint/Profile logging level that matches your privacy and audit requirements.                                              |
| NextDNS CLI / router client        | Local agent or router integration that forwards DNS to NextDNS and may attach client metadata.                                                                     | `ctrld`, Control D's command-line daemon, or native OS/router deployment methods.                                                                                                 |

## Migration Steps

### 1. Inventory NextDNS

Before changing DNS, record the current NextDNS setup:

- All configuration/profile IDs.
- Which devices, routers, offices, users, or networks use each profile.
- Enabled security settings.
- Enabled privacy blocklists.
- Parental controls and service/category blocks.
- Allowlist and denylist entries.
- Rewrites and any private/local DNS names.
- Linked IPs and Dynamic DNS integrations.
- Logging and analytics retention preferences.
- Router, OS, browser, and mobile deployment methods.

Keep the current NextDNS resolver hostnames and configuration IDs until the Control D deployment is verified. They are useful rollback information.

### 2. Create Matching Control D Profiles

Create one Control D Profile for each NextDNS configuration that needs distinct policy behavior.

Example naming convention:

```text
NextDNS Migration - Staff
NextDNS Migration - Guest WiFi
NextDNS Migration - Kids
```

If multiple NextDNS profiles differ only by a few exceptions, consider using a shared baseline Profile plus Profile-specific Custom Rules. Keep the structure simple enough that your team can operate it after the migration.

### 3. Recreate Filters and Services

Map broad NextDNS settings to Control D features:

- Use [Filters](doc:filters) for malware, phishing, ads, trackers, content categories, and third-party filter lists.
- Use [Services](doc:services) for app/service-level rules where Control D has a matching service.
- Use [Custom Rules](doc:custom-rules) when a NextDNS setting is really a specific domain rule.

Do not assume that category names or third-party blocklists behave identically across providers. Start with the closest matching Control D options, then test the domains and apps that matter to your environment.

### 4. Import Allowlist and Denylist Entries

For each NextDNS profile:

1. Export or copy the Allowlist and Denylist.
2. Normalize each list to one domain per line.
3. Remove protocols, URL paths, quotes, comments, blank rows, and duplicates.
4. Import allow entries as **BYPASS** Custom Rules.
5. Import deny entries as **BLOCK** Custom Rules.
6. Keep allow and block rules in separate folders.

Control D Custom Rules expect domains or subdomains, not full URLs. If a NextDNS rule depends on a URL path, query string, or non-DNS condition, treat it as a review item rather than importing it blindly.

### 5. Recreate Rewrites and Local DNS Behavior

NextDNS rewrites often mix two different use cases:

- Public-domain overrides that should resolve to a specific public IP or target.
- Private/internal names for home labs, offices, Active Directory, or split-horizon DNS.

Move the first group to Control D Custom Rules where the target is appropriate. For private/internal DNS, verify the intended resolver path first. Depending on your environment, this may belong in local DNS forwarding, Active Directory integration, router DNS, or a `ctrld` custom configuration instead of a public Control D rule.

### 6. Choose the Deployment Method

Common migration paths:

- **Router or firewall:** create a Control D Endpoint for the network, then deploy Control D resolver settings or `ctrld` on the router/firewall.
- **Roaming devices:** create Endpoint/deployment groups and use OS profiles, MDM, browser settings, or `ctrld` depending on platform.
- **Legacy DNS:** use Control D legacy resolver IPs only when the source IP can be authorized reliably. Dynamic networks should use encrypted DNS or a heartbeat/Dynamic DNS workflow.
- **Browser DoH:** update browser-managed DNS settings if browsers currently point directly at NextDNS.

For broad network migrations, start with one test Endpoint and a small user group before changing DHCP, router, firewall, MDM, or browser policy for everyone.

## Using `ctrld` NextDNS Mode as a Bridge

If you currently use the NextDNS CLI or router integration, you do not have to change both the local daemon and the DNS provider at the same time.

`ctrld` supports **NextDNS Mode** with `ctrld` v1.3.2 or newer. In this mode, `ctrld` forwards traffic to a NextDNS profile while relaying client metadata such as MAC address, IP address, and hostname, similar to the native NextDNS app.

Install `ctrld`, then start it with your existing NextDNS profile ID:

```bash
ctrld start --nextdns NEXTDNS_PROFILE_ID
```

The generated config is usually written under `/etc/controld/ctrld.toml`, though the exact path can differ by platform. By default, NextDNS Mode sends traffic to the selected NextDNS profile over DoH3 and appends LAN metadata when supported.

Use this bridge when you want to:

- Validate that `ctrld` installs and starts correctly on the router, firewall, server, or endpoint.
- Confirm local clients are discovered correctly with `ctrld clients list`.
- Keep NextDNS policy behavior unchanged while you test the local DNS listener.
- Reduce the final cutover to changing the upstream/profile target from NextDNS to Control D.

**Then switch to Control D**: Once `ctrld` is working locally, create the matching Control D Endpoint and switch the deployment to the Control D resolver/provisioning command for that Endpoint.

> The full `ctrld` NextDNS Mode reference is available in the [`ctrld` wiki](https://github.com/Control-D-Inc/ctrld/wiki/NextDNS-Mode).

## Cutover Checklist

Before switching production DNS:

- Confirm each Control D Profile is enforced on the intended Endpoint.
- Verify allowlist entries became BYPASS Custom Rules.
- Verify denylist entries became BLOCK Custom Rules.
- Test important business, school, family, or customer workflows.
- Check [Activity Log](doc:activity-log) for expected queries, blocks, bypasses, and Endpoint names.
- Compare a few known blocked and allowed domains against the old NextDNS behavior.
- Verify private/local names still resolve through the intended resolver path.
- Confirm browser DoH, mobile private DNS, VPN clients, and router DHCP settings are not still pointing at NextDNS.
- Keep the old NextDNS configuration available until the Control D deployment has run cleanly for a few days.

## Rollback

Keep the previous NextDNS setup documented until the migration is complete:

- NextDNS profile/configuration IDs.
- Resolver hostnames or URLs.
- Linked IP settings.
- Router, DHCP, MDM, browser, and OS settings that were changed.
- Any old NextDNS client/service commands.

Rollback is usually just reversing the DNS settings to the previous NextDNS resolver or restarting the previous client. If you used `ctrld` NextDNS Mode as a bridge, you can point `ctrld` back at the NextDNS profile while you adjust the Control D Profile or Endpoint configuration.
