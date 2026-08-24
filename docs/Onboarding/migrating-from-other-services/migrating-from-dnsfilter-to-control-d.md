---
title: Migrating from DNSFilter to Control D
excerpt: >-
  Migrate from DNSFilter to Control D by rebuilding your filtering policies,
  organizations, allow lists, block lists, and deployment workflow, with a final
  verification step before cutover.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Working Model

Most DNS filtering migrations are a concept-mapping exercise. For each policy in the old platform, create the equivalent Control D Profile, recreate the broad filters, import the allow/block exceptions as Custom Rules, then attach that Profile to the right Control D Endpoints.

## DNSFilter to Control D: Concept Map

| DNSFilter Concept                     | What It Means in DNSFilter                                                                                                                                                                                                       | Control D Equivalent                                                                                                                                                                      |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Filtering Policy                      | The cloud policy that controls categories, threats, AppAware, privacy settings, allow lists, block lists, Labs, and schedules. DNSFilter says policies can be applied to Sites, Relays, Roaming Clients, Collections, and Users. | Control D Profile. Profiles are policies that contain Filters, Services, Custom Rules, and Profile Options. A Profile only takes effect when enforced on an Endpoint.                     |
| Site                                  | A DNSFilter container used with Roaming Clients. DNSFilter says Sites connect filtering policies, local domains/resolvers, and DNS query/billing attribution.                                                                    | Usually a Control D Endpoint, or a group of Endpoints, depending on deployment shape. If the DNSFilter Site represents one office/network resolver, create one Endpoint for that network. |
| Roaming Client                        | DNSFilter endpoint agent that applies the assigned policy wherever the device connects.                                                                                                                                          | Control D Endpoint using the relevant deployment method, for example ctrld, OS profiles, MDM, router, or resolver-based deployment.                                                       |
| Categories / Threats / Privacy / Labs | DNSFilter broad blocking toggles.                                                                                                                                                                                                | Control D Filters. Enable the closest matching native or third-party Filters inside the matching Profile.                                                                                 |
| AppAware app blocking                 | DNSFilter app-level domain bundles.                                                                                                                                                                                              | Control D Services where there is a matching service. If there is no matching Service, recreate with Custom Rules.                                                                        |
| Policy Allow List                     | Per-policy explicit domains that DNSFilter allows. DNSFilter says Allow Lists always win in its hierarchy.                                                                                                                       | BYPASS Custom Rules in the matching Control D Profile. Custom Rules are evaluated before Services and Filters, so this is the right place for exceptions.                                 |
| Policy Block List                     | Per-policy explicit domains that DNSFilter blocks.                                                                                                                                                                               | BLOCK Custom Rules in the matching Control D Profile. Put them in a clearly named folder like "DNSFilter Block List - Policy Name".                                                       |
| Universal Allow / Block Lists         | DNSFilter blanket lists across all Filtering Policies.                                                                                                                                                                           | Shared/base Control D Profile or shared Custom Rules folder strategy, enforced wherever the global behavior should apply. Keep allow and block lists separate.                            |
| Local Domains and Resolvers           | DNSFilter Site-level local DNS handling.                                                                                                                                                                                         | Control D Active Directory/local domain handling. Use split horizon DNS or mirror private DNS records with Custom Rules, depending on the environment.                                    |

## Migration Steps<br />

### 1. Inventory DNSFilter

1. Export a list of Filtering Policies.
2. For each policy, record enabled Categories, Threats, AppAware apps, Privacy settings, Labs options, schedules, and where the policy is applied.
3. Record Sites, Roaming Clients, Relays, Collections, Users, and any local domains/resolvers.

### 2. Create One Control D Profile per DNSFilter Filtering Policy

1. Name it after the original policy, for example `DNSFilter Migration - Staff`.
2. If DNSFilter has a global Universal Allow or Block List, create a shared/base Control D Profile or consistent rule folder plan before recreating policy-specific rules.

### 3. Map Filters

1. DNSFilter Categories, Threats, and Privacy settings usually map to Control D Filters.
2. DNSFilter AppAware usually maps to Control D Services where a matching Service exists.
3. Anything without a clean match becomes a Custom Rule set.
4. Do not claim a one-to-one category match unless the category names and behavior are close enough. Mark unclear mappings for review.

### 4. Export DNSFilter Allow/Block Rules

1. In DNSFilter, export each policy Allow List and Block List as CSV from the policy's Allow List or Block List page.
2. DNSFilter notes and categories are not included in that export, so keep a screenshot or separate admin note if those matter.
3. Export Universal Allow and Block Lists separately if used.

### 5. Normalize Rules for Control D

1. Convert each CSV to a plain text list, one domain per line.
2. Strip protocols, paths, quotes, blank rows, notes, and duplicate rows.
3. Keep allow and block lists separate.
4. Keep policy-level and universal lists separate.
5. Control D custom rules require domains or subdomains (FQDNs), not full URLs. Preserve domains and subdomains. Wildcards are supported for broader matches (e.g., \*.example.com). Review TLD-only entries carefully before importing.

### 6. Import into Control D Custom Rules

1. For DNSFilter Allow Lists, create BYPASS Custom Rules.
2. For DNSFilter Block Lists, create BLOCK Custom Rules.
3. Put rules in named folders so marketing/support can explain the migration cleanly later, for example `DNSFilter Allow List - Staff` and `DNSFilter Block List - Staff`.

### 7. Create or Assign Control D Endpoints

1. For each DNSFilter Site or Roaming Client deployment group, create the matching Control D Endpoint(s).
2. Enforce the correct Profile on each Endpoint.
3. For bulk endpoint creation, use Control D's Add Multiple Endpoints flow or the deployment method that matches the customer environment.

### 8. Handle Active Directory and Local Domains

1. If endpoints will use ctrld or otherwise send all DNS to Control D, local AD domains may stop resolving unless handled.
2. Use the Control D Active Directory guide.
3. **Option A**: split horizon DNS, so local domains still resolve through internal DNS.
4. **Option B**: mirror private DNS records in Control D Custom Rules using Redirect to IP/hostname.
5. For the documented bypass approach, create a Control D Bypass folder and add wildcard BYPASS rules for AD domains, for example `*.example.local`.

### 9. Cut Over and Retire DNSFilter

Cut over in waves, starting with a small pilot. Validate each wave (Step 10) before you retire DNSFilter for that wave.

1. Export and retain your DNSFilter Query Log history and reports first. It does not migrate, and endpoints stop reporting to DNSFilter once they switch.
2. Switch one wave at a time to Control D, using the method that matches how it reaches DNSFilter:
   1. **Site forwarder**: change the forwarder (router, firewall, or domain controller) to send DNS to Control D instead of DNSFilter.
   2. **Relay**: switch the Site's DNS to Control D and stop the Relay forwarding to DNSFilter.
   3. **Roaming Client**: disable/remove the DNSFilter Roaming Client, then deploy Control D on the device (Step 7).
3. Retire DNSFilter for the wave only after it is validated (Step 10). For a Site forwarder or Relay, the switch above already does this. For Roaming Clients, remove the DNSFilter client from each device. Keep the wider DNSFilter policy and configuration intact until every wave is done.

### 10. Validate During Overlap

1. Define rollback first: for each wave, point the forwarder or Relay back to DNSFilter, or reinstall the DNSFilter Roaming Client. Keep DNSFilter live until the wave is validated.
2. Set success criteria per wave and only move to the next once they are met.
3. Test representative users/devices from each migrated policy.
4. Confirm the intended Control D Profile is enforced on each Endpoint.
5. Confirm blocked categories behave as expected.
6. Confirm allow-list exceptions win over Filters.
7. Confirm local AD resources and internal names resolve.
8. Confirm the wave in Control D's Activity Log. Compare against your exported DNSFilter history as the "before" baseline.

<br />
