---
title: Sync Transactions
excerpt: >-
  This guide picks up after ERP onboarding is complete. If you haven't completed
  onboarding yet, start with [Onboard ERP](/docs/onboard-erp). It covers how
  Paylocity for Finance generates ledger entries from transactions, how to
  retrieve them, how to report sync results back, and how ledger entry
  visibility changes based on sync status.
---
**1 - Begin processing transactions in Paylocity for Finance**

- Once onboarding and ERP integration is complete, users can now operate Paylocity for Finance to create spend requests, make card payments, submit expense reports, and process vendor bills and payments

- For every completed and approved transaction, Paylocity for Finance automatically generates ledger entries representing the full accounting impact. These entries appear in the accounting area of the product, where they can be reviewed by an accountant before syncing.

**2 - Retrieve ledger entries**

- After ledger entries are reviewed, the user initiates a sync in the Paylocity for Finance web app. This action moves the entries into the `sync_ready` state, making them available for retrieval through the **Ledger Entries GET API**.

- If preferred, you can subscribe to a webhook that fires automatically whenever a ledger entry transitions to the `sync_ready` state. This allows your ERP to post the entries to the general ledger more promptly.

- Each ledger entry includes, at the minimum, transaction date, amount, accounts, tags, subsidiary, and vendor, enabling the ERP to accurately reconstruct the full accounting impact.

- _Note: Only ledger entries with a status of_ `_sync_ready_` _are returned through the GET endpoint. This ensures data efficiency and prevents redundant transfers._

**3 - Save sync results back to Paylocity for Finance**

- After posting the ledger entries to the ERP's general ledger, the ERP should call the **Ledger Entries POST API** to record the outcome. This API accepts the status:

  - `sync_complete`

  - `sync_error`
- Recording the sync result updates the ledger entry's state within Paylocity for Finance and provides users with visibility into its sync lifecycle.

**4 - Manage ledger entry visibility based on sync status**

- Paylocity for Finance displays ledger entries in different states depending on the sync result:

  - **Completed syncs** (`status` = `sync_complete`)

    - Entries appear in the Paylocity for Finance UI on the Sync Complete page, which contains ledger entries that have been successfully synced.

    - These entries are not returned in future **Ledger Entries GET** requests.
  - **Errored syncs** (`status` =`sync_error`)

    - Entries appear in the Paylocity for Finance UI on the Pending Review page for user review and troubleshooting.

    - Users must resolve the issues and mark them ready for sync again.

    - Once updated, they will be included in future **Ledger Entries GET** requests.

<br />