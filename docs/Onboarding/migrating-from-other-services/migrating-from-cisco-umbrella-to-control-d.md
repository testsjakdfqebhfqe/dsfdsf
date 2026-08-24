---
title: Migrating from Cisco Umbrella to Control D
excerpt: >-
  Migrate from Cisco Umbrella to Control D by recreating your DNS policies,
  identity-based rules, roaming client setup, and forwarding configuration, then
  testing everything before switching production traffic.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Working Model

Most Cisco Umbrella DNS-layer migrations are a concept-mapping exercise. For each Umbrella DNS Policy, create the equivalent Control D Profile, recreate the broad security and content controls, import allow/block exceptions as Custom Rules, then attach that Profile to the right Control D Endpoints.

This document is focused on Umbrella DNS-layer security. If the customer is also using Umbrella SWG, firewall, DLP, CASB, RBI, or other Secure Access features, scope those separately. Those controls may not be DNS-policy migrations.

## Cisco Umbrella to Control D: Concept Map

| Cisco Umbrella Concept                                                                         | What It Means in Cisco Umbrella                                                                                                                                                                                                                                                                                                                        | Control D Equivalent                                                                                                                                                                                                                              |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DNS Policy                                                                                     | The policy that applies DNS-layer visibility, security, and access controls to Umbrella identities. Umbrella policies can include security categories, content categories, application settings, destination lists, logging, and related policy components. Umbrella applies the first matching policy to an identity, then stops evaluating policies. | Control D Profile. Profiles contain Filters, Services, Custom Rules, and Profile Options. A Profile only takes effect when enforced on an Endpoint.                                                                                               |
| Default Policy                                                                                 | Umbrella's catch-all DNS policy when no other DNS policy matches an identity.                                                                                                                                                                                                                                                                          | A baseline Control D Profile enforced on any Endpoint that should receive default protection. Keep this separate from special-case Profiles unless the customer has a very small policy set.                                                      |
| Identity                                                                                       | An internet-capable entity Umbrella protects through policies and reports. Examples include networks, roaming computers, network devices, mobile devices, AD users, AD groups, and other deployment-specific identities.                                                                                                                               | Usually a Control D Endpoint, or a group of Endpoints, depending on deployment shape. The practical mapping is: one Control D Endpoint per office network, device, router, resolver, or deployment group that needs distinct policy or reporting. |
| Network identity                                                                               | A public egress IP or network location protected by Umbrella DNS.                                                                                                                                                                                                                                                                                      | Control D Endpoint for that network or resolver-based deployment. Enforce the matching Profile on the Endpoint.                                                                                                                                   |
| Roaming Computer / Umbrella Roaming Client / AnyConnect or Cisco Secure Client Umbrella module | Umbrella's roaming endpoint deployment that applies policy when the device leaves the protected network.                                                                                                                                                                                                                                               | Control D Endpoint using `ctrld`, OS profiles, MDM deployment, router deployment, or another supported endpoint deployment method.                                                                                                                |
| Roaming computer tags                                                                          | Umbrella grouping mechanism for roaming computers.                                                                                                                                                                                                                                                                                                     | Endpoint naming, folders, consistent metadata, or deployment groups. If tags drive policy assignment, create matching Endpoint groupings and enforce the relevant Profile.                                                                        |
| Virtual Appliance                                                                              | Umbrella on-network DNS forwarder used for internal identity visibility and AD-aware deployments.                                                                                                                                                                                                                                                      | Usually replaced by Control D Endpoints plus the local DNS/Active Directory workflow. If the VA is doing internal domain forwarding, handle that explicitly before cutover.                                                                       |
| Network Device                                                                                 | Umbrella deployment for supported network devices.                                                                                                                                                                                                                                                                                                     | Control D router, network, resolver, or `ctrld` deployment, depending on the customer environment.                                                                                                                                                |
| Security Settings / DNS Security Categories                                                    | Umbrella threat/security toggles such as malware, phishing, command-and-control, newly seen domains, and related security categories.                                                                                                                                                                                                                  | Control D Filters. Enable the closest matching native or third-party Filters inside the matching Profile. Do not claim a one-to-one category match unless the behavior is close enough.                                                           |
| Content Settings / Content Categories                                                          | Umbrella content-category blocking, for example adult content, gambling, social networking, and other web categories.                                                                                                                                                                                                                                  | Control D Filters. Map the closest matching categories and mark unclear mappings for review.                                                                                                                                                      |
| Application Settings                                                                           | Umbrella application-based destination groups used in DNS and Web policies.                                                                                                                                                                                                                                                                            | Control D Services where there is a matching service. If there is no matching Service, recreate with Custom Rules where DNS-level matching is possible.                                                                                           |
| Destination List                                                                               | Umbrella list of internet destinations such as domains, URLs, and CIDRs. Destination Lists are selected in DNS and Web policies.                                                                                                                                                                                                                       | Control D Custom Rules for domain-based allow/block behavior. Domains and subdomains map cleanly. URL-path entries and CIDRs need review because DNS rules do not see URL paths.                                                                  |
| Allow Destination List                                                                         | Umbrella allow list used to permit selected destinations.                                                                                                                                                                                                                                                                                              | BYPASS Custom Rules in the matching Control D Profile. Custom Rules are evaluated before Services and Filters, so this is the right place for DNS exceptions.                                                                                     |
| Block Destination List                                                                         | Umbrella block list used to deny selected destinations.                                                                                                                                                                                                                                                                                                | BLOCK Custom Rules in the matching Control D Profile. Put them in a clearly named folder like `Umbrella Block List - Policy Name`.                                                                                                                |
| Global Allow / Global Block List                                                               | Umbrella DNS Global Lists that apply across all DNS policies and identities.                                                                                                                                                                                                                                                                           | Shared/base Control D Profile or shared Custom Rules folder strategy, enforced wherever the global behavior should apply. Keep allow and block lists separate.                                                                                    |
| Internal Domains / local DNS forwarding                                                        | Umbrella local-domain handling, often tied to Virtual Appliances, protected networks, or internal resolvers.                                                                                                                                                                                                                                           | Control D Active Directory/local domain handling. Use split horizon DNS or mirror private DNS records with Custom Rules, depending on the environment.                                                                                            |
| Reports / Activity Search                                                                      | Umbrella reporting used to validate what policy matched and why a request was allowed or blocked.                                                                                                                                                                                                                                                      | Control D Activity Log / Analytics during validation and cutover.                                                                                                                                                                                 |

## **Check policy granularity before you migrate identities**

Umbrella with the Virtual Appliance and AD connector can apply policy and reporting per AD user and per AD group. Control D enforces policy at the Endpoint. If your Umbrella policies or reports depend on AD-user or AD-group identity, map where that granularity changes before cutover and decide how to preserve it, for example per-user endpoint deployment, or grouping by network or device where user-level distinction is not required. Do not assume a one-to-one identity match.

## Migration Steps

### 1. Inventory Cisco Umbrella

1. Export a list of DNS Policies, including the Default Policy.
2. For each policy, record assigned identities, policy order, enabled security categories, content categories, application settings, destination lists, logging settings, and any special policy components.
3. Record Networks, Roaming Computers, roaming client tags, Network Devices, Virtual Appliances, AD users/groups, mobile devices, and protected networks.
4. Record Global Allow and Global Block Lists if used.
5. Record internal domains, local resolvers, Virtual Appliance forwarding behavior, and any AD-dependent identity behavior.

### 2. Create One Control D Profile per Umbrella DNS Policy

1. Name it after the original policy, for example `Umbrella Migration - Staff`.
2. Preserve policy intent, not the exact Umbrella UI structure.
3. Because Umbrella uses first-match policy order, verify which identities actually receive each DNS Policy before recreating the policy set.
4. If Umbrella has Global Allow or Global Block Lists, create a shared/base Control D Profile or consistent rule folder plan before recreating policy-specific rules.

### 3. Map Broad Controls

1. Umbrella Security Categories usually map to Control D security Filters.
2. Umbrella Content Categories usually map to Control D content Filters.
3. Umbrella Application Settings usually map to Control D Services where a matching Service exists.
4. Anything without a clean match becomes a Custom Rule set where DNS matching is possible.
5. Do not claim a one-to-one category match unless the category names and behavior are close enough. Mark unclear mappings for review.

### 4. Export Umbrella Destination Lists

1. Export or copy each policy-level Allow Destination List and Block Destination List.
2. Export DNS Global Allow and DNS Global Block Lists separately if used.
3. Keep DNS-policy lists separate from Web-policy lists if the customer also uses Umbrella SIG/SWG. Web-policy URL path behavior may not be a DNS migration.
4. Preserve the source policy name for each list so the imported Control D rule folders are easy to explain later.

### 5. Normalize Rules for Control D

1. Convert each list to a plain text list, one domain per line.
2. Strip protocols, paths, quotes, blank rows, comments, and duplicate rows.
3. Keep allow and block lists separate.
4. Keep policy-level and global lists separate.
5. Preserve domains and subdomains.
6. Review URL-path entries before importing. DNS cannot match `/path` behavior.
7. Review CIDR/IP entries separately. Some belong in endpoint/network deployment, traffic steering, or a non-DNS control rather than a domain Custom Rule.

### 6. Import into Control D Custom Rules

1. For Umbrella Allow Destination Lists, create BYPASS Custom Rules.
2. For Umbrella Block Destination Lists, create BLOCK Custom Rules.
3. Put rules in named folders so marketing/support can explain the migration cleanly later, for example `Umbrella Allow List - Staff` and `Umbrella Block List - Staff`.
4. If a list came from a Global Allow or Global Block List, put it in a shared/base Profile or a shared folder strategy and enforce it consistently.

### 7. Create or Assign Control D Endpoints

1. For each Umbrella Network identity, create the matching Control D network/resolver Endpoint.
2. For roaming clients, create the matching Control D device Endpoints using the deployment method that fits the customer environment.
3. For router, network-device, or resolver deployments, use the matching Control D deployment method.
4. Enforce the correct Profile on each Endpoint.
5. For bulk endpoint creation, use Control D's Add Multiple Endpoints flow or the deployment method that matches the customer environment.

### 8. Handle Active Directory and Local Domains

1. If endpoints will use `ctrld` or otherwise send all DNS to Control D, local AD domains may stop resolving unless handled.
2. Use the Control D Active Directory guide.
3. **Option A**: split horizon DNS, so local domains still resolve through internal DNS.
4. **Option B**: mirror private DNS records in Control D Custom Rules using Redirect to IP/hostname.
5. For the documented bypass approach, create a Control D Bypass folder and add wildcard BYPASS rules for AD domains, for example `*.example.local`.
6. If Umbrella Virtual Appliances were forwarding internal domains or enabling AD-aware identity, test this area before broad cutover.

### 9. Cut Over and Retire Umbrella

Cut over in waves. Validate each wave (Step 10) during the overlap before you retire Umbrella for that wave.

1. Do not point production DNS at Control D while the Umbrella roaming client or VA is still active on the same device or network. Two active DNS agents on one device will conflict. Disable Umbrella as each endpoint cuts over (leave it installed so you can re-enable it to roll back).
2. If DNS egress is currently restricted to Umbrella resolver IPs at the firewall, allow Control D's resolver endpoints before cutover or DNS will fail.
3. Cut over in stages. Start with a small pilot group from one migrated policy, confirm behavior, then expand. Do not cut over everyone at once.
4. Run Umbrella and Control D in parallel across waves during the overlap window so you can compare resolution and revert quickly.
5. Uninstall the Umbrella roaming client (AnyConnect or Cisco Secure Client Umbrella module) and retire the Virtual Appliance only after the wave's endpoints are confirmed on Control D.
6. Export and retain Umbrella historical reports and logs before decommissioning. Umbrella reporting history does not migrate to Control D.

### 10. Validate During Overlap

1. Define rollback before you start. For each pilot or cutover wave, know how to revert: re-point DNS to Umbrella resolvers, or re-enable the Umbrella client on affected devices. Keep Umbrella live and untouched until the wave is validated.
2. Set clear success criteria per wave (categories block as expected, allow-list exceptions win, internal domains resolve, no unexpected outages) and only move to the next wave once they are met.
3. Test representative users/devices from each migrated policy.
4. Confirm the intended Control D Profile is enforced on each Endpoint.
5. Confirm blocked security and content categories behave as expected.
6. Confirm allow-list exceptions win over Filters.
7. Confirm block-list entries still block.
8. Confirm local AD resources and internal domains resolve.
9. Use Control D Activity Log / Analytics and Umbrella reporting during the overlap window.

###

<br />
