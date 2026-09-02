---
title: Getting Started
excerpt: Set up the welcome page for your API to help users make their first call.
api_config: getting-started
hidden: true
icon: icon-book1
---
# Airbase Public API

The Airbase Public API provides programmatic access to Airbase's financial operations platform. This collection contains the core APIs that enable a fully functional integration between your ERP and Airbase, covering the essential endpoints and behaviours required for a successful end-to-end implementation.

## Airbase-ERP Integration Model

Airbase follows a **bidirectional integration framework** with ERP systems. The integration consists of two primary data flows: ERP master data ingestion and ledger entry synchronisation. Together, these ensure that Airbase's spend workflows remain aligned with the ERP's accounting structure and that all financial activity in Airbase is accurately reflected in the general ledger.

- **ERP Master Data Ingestion** — Airbase receives master data from the ERP using the ERP's object APIs, including currencies, subsidiaries, accounts, financial dimensions, vendors, and employees. This data is used throughout the spend lifecycle to classify requests, enforce policies and approvals, and ensure transactions align with the ERP's accounting structure.

- **Ledger Entry Generation and Sync** — For every approved financial activity in Airbase, such as bill payments, reimbursements, and card transactions, Airbase generates ledger entries that capture the full accounting impact. These ledger entries are exposed through the Ledger Entry Sync APIs.

***

## Authentication

All API requests require a token in the `Authorization` header:

```
Authorization: Token <key>:<secret>
```

Generate API tokens in the Airbase web app under **Settings → Connections → Tokens & Webhooks**. Each API request must include this token to authenticate with the Airbase API. Once generated, copy the token and store it securely — it cannot be viewed again after you close the screen.

## Rate Limits

All endpoints are subject to a rate limit that applies across all Airbase APIs — not just the ERP Objects APIs. When the limit is exceeded, the API returns `429 Too Many Requests`. The response includes `X-RateLimit-Limit` (your per-minute limit) and `X-RateLimit-Remaining` (requests remaining in the current window) headers. This limit may be adjusted during onboarding once we understand the expected GL data throughput.

***

## Quickstart Guide

This guide walks you through the essential steps to prepare your environment and make your first API call.

**1 — Obtain an Airbase sandbox account**

- Request a sandbox account by contacting [ab-api@paylocity.com](mailto:ab-api@paylocity.com).
- A sandbox account is recommended for safely experimenting with API calls without affecting production data.

**2 — Generate access tokens**

- Go to **Settings → Connections → Tokens & Webhooks** and click **Generate Access Token**.
- Provide a name and expiry date, then click **Generate**.
- Copy and securely store the token. It cannot be viewed again once the screen is closed.

**3 — Get a copy of the API collection**

- If testing in Postman, request a fork of the collection and add it to your internal workspace.
- If testing outside Postman, export the collection and import it into your preferred API client.

**4 — Configure your API client (optional)**

Set the following variables:

| Variable       | Value                                                                             |
| -------------- | --------------------------------------------------------------------------------- |
| `access_token` | Your Airbase access token (format: `Token abc123xyz`)                             |
| `baseUrl`      | `https://api-stage.airbase.io` (sandbox) or `https://api.airbase.io` (production) |

Set authentication at the parent level by configuring **Auth Type** to **API Key**.

**5 — Begin interacting with the API**

- **ERP Master Data Ingestion** — Start making CRUD requests against the ERP objects APIs: Accounts, Currencies, Employees, Subsidiaries, Tags, Vendors. These endpoints synchronise ERP master data with Airbase.
- **Ledger Entry Retrieval** — Ledger Entry GET endpoints only return data when transactions exist in Airbase **and** their corresponding ledger entries are marked **ready for sync**. In the API, this is the `SYNC_READY` status. If no entries meet this condition, the endpoint returns an empty result.

***

## Building an Airbase-ERP Integration

This guide provides a detailed, end-to-end overview of the workflow required to build a complete integration. It covers how to establish the connection, sync ERP master data, process transactions, retrieve ledger entries, and manage the full sync lifecycle.

### Step 1 — Connect Airbase to the ERP during onboarding

- The integration is initially configured by the customer during their onboarding phase.
- An access token is generated in the Airbase web app as part of this process.
- The token is stored in the ERP and used to authorise API communication between the two systems.

### Step 2 — Push all ERP master data using POST API calls

- Before any additional configuration, ERP master data must be pushed into Airbase using the ERP master data APIs. This includes **accounts**, **subsidiaries**, **currencies**, **tags**, **vendors**, and **employees**.
- This step is mandatory and must be completed before transaction workflows can begin in Airbase.
- To keep ERP master data in sync, we recommend running a **scheduled job every 24 hours**. Keeping this up to date reduces sync errors and ensures accurate accounting downstream.

#### Sync Sessions

A **sync session** tracks the progress of an ERP master data push. Wrapping your entity sync in a session allows Airbase to accurately reflect which entities have been synced and to surface the sync status in the UI.

**Lifecycle:**

1. **Start a session** — Call `POST /v1/accounting/entity/sync` with `{ "action": "START" }` before pushing any entity data. This creates a new session in the `IN_PROGRESS` state and returns a `session_id`. Starting a new session automatically cancels any previously active session.
2. **Push entity data** — Use the ERP master data APIs to push accounts, subsidiaries, currencies, tags, vendors, and employees as normal.
3. **Complete the session** — Once all entity data has been pushed, call `PATCH /v1/accounting/entity/sync` with `{ "action": "COMPLETE" }`. This transitions the session to the `COMPLETE` state.
4. **Check session status** — At any point, call `GET /v1/accounting/entity/sync/` to retrieve the current session status.

**Session states:**

| State               | Description                         |
| ------------------- | ----------------------------------- |
| `IN_PROGRESS`       | A sync is currently underway.       |
| `COMPLETE`          | The session completed successfully. |
| `NO_ACTIVE_SESSION` | No session is currently active.     |

**Notes:**

- Sessions expire after **60 minutes** if not completed. Always call the complete endpoint once your entity push finishes.
- Only one session can be active per company at a time. Starting a new session will override any existing in-progress session.

### Step 3 — Configure GL account mappings in Airbase

- After master data is synced, the user completes the integration setup workflow in the Airbase web app. This involves selecting the appropriate GL accounts to be used in spend workflows and transaction categorisations.
- These mappings can be viewed and updated at any time after onboarding.

### Step 4 — Begin processing transactions in Airbase

- Once onboarding and ERP integration is complete, users can operate Airbase to create spend requests, make card payments, submit expense reports, and process vendor bills and payments.
- For every completed and approved transaction, Airbase automatically generates ledger entries representing the full accounting impact. These entries appear in the accounting area of the product, where they can be reviewed by an accountant before syncing.

### Step 5 — Retrieve ledger entries

- After ledger entries are reviewed, the user initiates a sync in the Airbase web app. This moves entries into the `SYNC_READY` state, making them available via the **Ledger Entries GET API**.
- Alternatively, subscribe to a webhook that fires automatically when entries transition to `sync_ready`. This allows your ERP to post entries to the general ledger more promptly.
- Each ledger entry includes, at minimum: transaction date, amount, accounts, tags, subsidiary, and vendor — enabling the ERP to reconstruct the full accounting impact.
- Only entries with `status=SYNC_READY` are returned through the GET endpoint. This ensures data efficiency and prevents redundant transfers.

### Step 6 — Save sync results back to Airbase

- After posting entries to the ERP's general ledger, call the **Ledger Entries PATCH API** to record the outcome:
  - `sync_complete` — entry synced successfully
  - `sync_error` — sync failed with an error
- Recording the sync result updates the entry's state within Airbase and provides users with visibility into its sync lifecycle.

### Step 7 — Manage ledger entry visibility based on sync status

Airbase displays ledger entries in different states depending on the sync result:

- **Completed syncs** (`status = SYNC_COMPLETE`) — Entries appear on the **Sync Complete** page in the Airbase UI. They are not returned in future GET requests.
- **Errored syncs** (`status = SYNC_ERROR`) — Entries appear on the **Pending Review** page for user review and troubleshooting. Users must resolve the issues and mark them ready for sync again. Once updated, they will be included in future GET requests.

***

## Webhooks

Airbase provides webhook notifications when ledger entries transition to a sync-ready state. See the **Webhooks** section for full details on events, payload structure, setup instructions, and best practices.
