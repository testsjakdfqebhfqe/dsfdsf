---
title: Statistics
excerpt: >-
  Get a clear picture of DNS activity across your organization, spot anomalies
  fast, and drill down with one click.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Terminology

Below is a general glossary of terminology used on the Statistics page.

| Term                                | Meaning                                                                   |
| ----------------------------------- | ------------------------------------------------------------------------- |
| **Refine**                          | Narrow the data shown (e.g., by action, endpoint, domain, location, ASN). |
| **Filter**                          | A blocklist category (product feature), not a UI control.                 |
| **Endpoint**                        | A device that enforces one or more Profiles.                              |
| **Profile**                         | A policy set of rules enforced by one or more Endpoints.                  |
| **Organization / Sub-Organization** | Your tenant hierarchy; selection controls scope.                          |
| **Service**                         | A first-class service (e.g., “YouTube”) that rules can target.            |

> **Note:** If an Endpoint enforces multiple Profiles and you select a single Profile, you’ll see only the queries **enforced by that Profile**, not all queries from that Endpoint.

***

## Top bar

<Image border={false} src="https://files.readme.io/a000b1e3b7a5554bdc38a3bb8a247c08bfdedd3e1e56bcacd0cbf07fefa74be5-image.png" />

### Profile selector

Pick **All Profiles** or a single Profile to scope all charts and lists.

### Time range

Options: **Last hour, Last day, Last week, Last month, Last year, Custom** (up to 1 year back).

### Active refinements

<Image border={false} src="https://files.readme.io/f2af400ba6c3e254a15f8feed6f3d93f332cfb389185d6121d429b9f34ce3c24-image.png" />

Shows every refinement currently applied. Add more by hovering elements and clicking **Refine**.

You can refine by:

* **Action:** Blocked, Bypassed, Redirected
* **Filter**
* **Service**
* **Domain**
* **Endpoint**
* **Source location (Country)**
* **Destination location (Country)**
* **Network source (ASN)**
* **Network destination (ASN)**

Click a pill to remove it.

***

## Key metrics

### Action summary

<Image border={false} src="https://files.readme.io/b3351197ef4c4675d69d97caffd56e46e6d34fb4153e5f4f2b39795a1d0064d1-image.png" />

**Blocked**, **Bypassed**, **Redirected**, and **Total queries**.

* Click a slice/legend to **Refine** by that action.
* Click **Total** to clear action refinements.

### Security overview

<Image align="center" border={false} src="https://files.readme.io/4563176e73cd792a750e091f0de07b1990e7d83ab0b560554157afafe4478247-Overview.png" />

Bars that should trend near 100%:

* **Encrypted DNS** - share of queries over DoH/DoT/DoQ. If you have Some Analytics selected for any endpoints, this will not currently reflect reality, since we don't store the protocol for each query in this case
* **Benign Blocks** - percentage of blocked DNS queries attributable to non-security Filters (Filters other than Malware and Phishing). A value of 100% means none of your blocked queries matched the Malware or Phishing Filters. It is normal for some malicious domains to be blocked during everyday browsing, so 97% or higher is generally expected and still indicates a healthy network. If this value falls below 90%, investigate whether a device is making unusual queries. A low value does not by itself prove that a device is infected.
* **Home Country Traffic** - share of queries from your chosen home countries (manage via dropdown; up to 3 flags shown)

All metrics respect the time range and refinements.

***

## Traffic chart

<Image border={false} src="https://files.readme.io/8dc53d39ad873eb760bfa266fccb9f4b25371fed48e418c53e4f230f23e2d36a-image.png" />

Interactive multi-series line chart:

* **Green** = Bypassed, **Red** = Blocked, **Yellow** = Redirected
* Click-drag a window to update the whole page
* When refined by **Action**, the Y-axis auto-scales to that series

***

## Endpoints overview

<Image align="center" border={false} width="300px" src="https://files.readme.io/fce4f0be956bfc957f7bfcfb42b9872e5ec39ecaa75b4ac4e8662a59dcf221d8-image.png" />

Ranked list (top 10; search for others) of Endpoints in the selected **Organization** (excludes Sub-Organizations if you are viewing a Parent Organization).

Each row shows:

* **Endpoint name**
* **Endpoint last active time**
* **Clients connected**
* **Total queries** OR **Trend** - the Trend percentage shows comparison of queries made over the period selected vs an equal length period immediately before it
* **Most active Filter** for that Endpoint

Hover to **Refine** by Endpoint.

***

## Clients overview

<Image align="center" border={false} width="300px" src="https://files.readme.io/4cbf00783ee22f042acc59863f310f099dbfb19592359075eeb958827db43606-image.png" />

<br />

Appears when there is a Refinement selected for an individual Endpoint. This section has the same layout as Endpoints, minus “Clients connected”.

Each row shows:

* **Total queries** and **% of Endpoint total**
* **Blocked vs typical** — current vs baseline
* **Most active Filter**

Hover to **Refine** by Client.

***

## Top actions

Tabs affect only the three boxes in this section.

<Image border={false} src="https://files.readme.io/3c09f9a6ac1e6ef378deb5039170f5ea7db9ab7e9d31ceacedcb89c8adf4ba43-image.png" />

### Blocked

* **Filters** - top 10 Filter categories by share of **Filter-blocked** queries
* **Services** - top 10 by share of **Service-blocked** queries
* **Domains** - top 10 by share of **all blocked** queries

  * Hover a domain → **Refine** to **TLD / apex / full domain**

### Bypassed

* **Services** - top 10 by share of **Service-bypassed** queries (overrides only; often small)
* **Domains** - top 10 by share of **all bypassed** queries

  * Hover a domain → **Refine** to **TLD / apex / full domain**

### Redirected

* **Services** - top 10 by share of **Service-redirected** queries
* **Domains** - top 10 by share of **all redirected** queries

  * Hover a domain → **Refine** to **TLD / apex / full domain**

***

## Geography and networks (map)

<Image border={false} src="https://files.readme.io/e246bd3e3f2ae7f824abb72b3a4f5d1039aad37c07bcc6ca263d7107c4c11ca8-image.png" />

<br />

* **Sources** - top 10 origin countries
* **Destinations** -  top 10 destination countries
* **Network sources** (list only) - top 10 originating ASNs
* **Network destinations** (list only) - top 10 destination ASNs

Hover any item to **Refine**. On the map, white countries are clickable (adds a refinement and highlights the country).

***

## Refinement behavior and scope

* Refinements stack with **AND** logic
* Clearing the **Action** refinement returns charts to all actions
* Profile selection limits data to **queries enforced by that Profile**

***

## Common tasks

* **See one Endpoint:** Endpoints → hover → **Refine**
* **Investigate a spike:** Drag over the spike → review **Top actions** and **Endpoints**
* **Trim noisy countries:** Geography → click countries to refine by **Source** or **Destination**

***

## Data Availability Notice

Since our new Analytics system has only been ingesting data since April 2025, you will not see data older than that on this page. If you'd like to get this older data (from the previous Analytics system), please contact support.
