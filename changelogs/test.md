---
title: test
author: Oleh Shumov
hidden: true
published_at: '2026-10-22T06:58:47.479Z'
---
Changes between 6 November and 4 December 2026

<div class="customTab"></div>

<summary class="tabContent" id="New features">

### Core banking - XXXXX

#### New

xxxxxx

{/* Arthur, https://pismolabs.atlassian.net/browse/PISMO-XXXXX */}

### Card issuing - XXXXX

#### New

xxxxxx

{/* Paul, https://pismolabs.atlassian.net/browse/PISMO-XXXXX */}

</summary>

<summary class="tabContent" id="Core platform">

### Accounting

#### New

xxxxxx

{/* Kristina, https://pismolabs.atlassian.net/browse/PISMO-XXXXX */}

### Client webhooks

#### Docs

xxxxxx

### General

#### Updated

xxxxxxx

### Migrations

#### Docs

Transaction type mappings in the [Migrate balances ](https://developers.pismo.io/pismo-docs/reference/postbalancecontrolv1)endpoint have been updated to map `ACCRUABLE_NOTFINEABLE` to transaction type `6902`, and `NOTACCRUABLE_FINEABLE` to transaction type `6903`.&#x20;

{/* Stacey, https://pismolabs.atlassian.net/browse/PISMO-482680?atlOrigin=eyJpIjoiY2UzM2FkM2Q1OTM3NGNiOTk0NmJjYWJjOTJlOWE0NjciLCJwIjoiaiJ9 */}

#### Docs

The example card numbers on the [Migrations overview](https://developers.pismo.io/pismo-docs/docs/migrations-overview#migration-using-file-upload) page were updated to remove any potential PII content to better align with Pismo business practices and standards.

{/* Stacey, https://pismolabs.atlassian.net/browse/PISMO-479731?atlOrigin=eyJpIjoiYmFlNmI1Yjc0MDQyNDY4NDhkODBmZDBhMDg4OThiMTEiLCJwIjoiaiJ9 */}

#### **Updated**

The [Token migration](https://developers.pismo.io/pismo-docs/reference/posttokensv1) endpoint was updated to replace devices_binding with consume_devices for indicating whether a token is bound to a device.

{/* Stacey, https://pismolabs.atlassian.net/browse/PISMO-393177?atlOrigin=eyJpIjoiMDI0MGUwMDY1NTJiNGZkMDg2ODJhZjEzNzY4YTgzYTgiLCJwIjoiaiJ9}

#### **Updated**

Added F as a supported `token_type` value for Mastercard Card on File tokens to [Token migration](https://developers.pismo.io/pismo-docs/reference/posttokensv1) endpoint.

{/* Stacey, https://pismolabs.atlassian.net/browse/PISMO-457864?atlOrigin=eyJpIjoiMDQ3ODBhZTYwY2Q4NDAwMGI0ZmNiYjIzY2I5Njg4ODIiLCJwIjoiaiJ9}

### Payments

#### Update

xxxxxx

### Programs

#### Docs

xxxxxxxx

### Rates and fees

#### Updated

xxxxxxxx

{/* MK, https://pismolabs.atlassian.net/browse/PISMO-XXXXX */}

### Setup

#### Update

xxxxxxx

#### Docs

xxxxxxxxx

{/* Kristina, https://pismolabs.atlassian.net/browse/PISMO-XXXXX */}

### Support

#### Docs

xxxxx

### Transactions

#### Docs

xxxxx

</summary>

<summary class="tabContent" id="Data and reporting">

### Events

#### Updated

xxxxxxx

### Reports

#### Updated

xxxxxx

</summary>

<summary class="tabContent" id="Core banking">

### Banking operations

#### Updated

The behavior of the `account_creation_datetime` field in the [Open deposit account](ref:interest-bearing-v1-deposit-account-open) endpoint was clarified. The clarifications include accepted RFC 3339 format, division time zone handling, default behavior when omitted, and the impact of retroactive timestamps on maturity date and interest cycle calculations.

#### Updated

The behavior of the [Detach deposit from account](ref:interest-bearing-v1-deposit-detach-account) endpoint for `409 Conflict` responses was elaborated. It was clarified that a product cannot be detached if it has already been detached from the account or if the account closure process is in progress. Either of these error codes is generated when `409 Conflict` is returned.

- `EIBACC0114` when the product is already detached  
- `EIBACC0419` while account closure is underway 

#### Updated

A new endpoint, [Get cycle snapshot history for deposit account \[beta\]](ref:interest-bearing-v2-get-cycle-snapshot), is now available in beta release. It retrieves the complete deposit account cycle history, including cycle status and active-cycle identification, pagination behavior, timezone-based lifecycle date calculations, and retention rules for open and closed accounts.

#### Updated

In the [Get cycle snapshot for deposit account](ref:interest-bearing-v1-get-cycle-snapshot) endpoint, the source of the `current_` and `previous_` fields was clarified. The `current_` fields come from the most recent cycle, and the `previous_` fields come from the cycle immediately before it. When the account is in its first cycle, the `previous_*` fields are empty and `previous_calendar_maturity_date` is `null`.&#x20;

#### Updated

The [beta] tag was removed from the following endpoints.
  * [Get interest account](ref:get-v1-interest-account)
  * [Patch interest account](ref:patch-v1-interest-account)

#### Updated

The following new events are now available in beta release.

* [Interest accrual instruction failed](https://developers.pismo.io/events/docs/interest-engine-interest-accrual-instruction-failure-1)
* [Interest accrual instruction succeeded](http://developers.pismo.io/events/docs/interest-engine-interest-accrual-instruction-success-1)

### Instant payments

#### New

xxxxx

### Payment rails

#### Docs

xxxxxx

### Transaction banking

#### Updated

A new `409` error message, `WRFO0024`: `Restricted fund has an operation in progress`, was added to the following endpoints. This error is generated when clients manually increase funds while the restricted fund operation is still in progress.&#x20;

- [Release restriction](ref:patch-corporate-v1-restricted-funds)  
- [Update restriction](ref:patch-corporate-v2-restricted-funds)   

#### Updated

The following error codes were added to ensure clients receive errors consistent with the documentation. These changes were made.

`WCPT0019`: `Back business dating is disabled` was added to the following endpoints.

- [Create check posting](ref:corporate-post-v1-checks)
- [Release check](ref:post-corporate-v1-checks-release)  
- [Cancel check](ref:post-corporate-v1-checks-checkid-cancel)

`WCPT0020`: `Check posting was concurrently modified` was added to the following endpoints.

- [Cancel check](ref:post-corporate-v1-checks-checkid-cancel)  
- [Release check](ref:post-corporate-v1-checks-release)   

#### Updated

The description for `cycle_closing_time` was updated in the following endpoints. The description now clarifies that each account's cycle closes at the division's configured cycle closing time, using the timezone of the division hierarchy (as set by the `timezone` field in the [Create division](ref:post-division-v2) endpoint), and defaults to UTC when no timezone is configured. The [Get division](ref:get-division-by-code-v2) by code endpoint returns only the timezone set directly on the division, not one inherited from a parent division.&#x20;

- [Create account balance history config v1](ref:post-account-balance-history-configuration) (request and response)
- [Get account balance history config v1](ref:get-account-balance-history-configuration) (response)

#### Updated

Clarified cycle closing time and timezone behavior. Each account's cycle closes at the cycle closing time configured for its division, organization, or program, in the account's timezone as set by the timezone field in Create division. Cycle closing events use the target entity's timezone, with each defaulting to UTC when no timezone is configured. This update affects these endpoints.

[https://developers.pismo.io/pismo-docs/reference/post-account-balance-history-configv2](https://developers.pismo.io/pismo-docs/reference/post-account-balance-history-configv2)  (request)

[https://developers.pismo.io/pismo-docs/reference/patch-account-balances-history-configv2](https://developers.pismo.io/pismo-docs/reference/patch-account-balances-history-configv2)  (request)

[https://developers.pismo.io/pismo-docs/reference/get-account-balance-history-config-by-id-v2](https://developers.pismo.io/pismo-docs/reference/get-account-balance-history-config-by-id-v2) (response)

[https://developers.pismo.io/pismo-docs/reference/get-account-balance-history-config-by-target-v2](https://developers.pismo.io/pismo-docs/reference/get-account-balance-history-config-by-target-v2) (response)

</summary>

<summary class="tabContent" id="Card issuing">

### Cards

#### Updated

xxxxxx

### Disputes

#### New

xxxxxx

### Network transactions

#### Updated

xxxxx

</summary>

<summary class="tabContent" id="Resources">

### Control Center

#### Updated

xxxxxx

</summary>