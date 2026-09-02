---
title: ERP integration overview
excerpt: >-
  Understand how Paylocity for Finance exchanges ERP master data and
  synchronises accounting entries with an ERP system.
deprecated: false
hidden: false
metadata:
  robots: index
---
Paylocity for Finance uses a bidirectional integration model to keep spend workflows aligned with the ERP's accounting structure and reflect Paylocity for Finance activity in the general ledger.

<Callout icon="⚠️" theme="info">
  ### Early Access

  ERP Integration APIs are available through the Paylocity for Finance Early Access programme. Response fields, validation rules, and behaviour may change before general availability.
</Callout>

## Integration model

The integration consists of two primary data flows:

1. **ERP master data flows into Paylocity for Finance.**
2. **Accounting entries flow from Paylocity for Finance to the ERP.**

Together, these flows give Paylocity for Finance the accounting context needed to classify spend and give the ERP the accounting records needed to reflect completed financial activity.


<Image src="https://files.readme.io/fd1c19c2cdc098f8e751232322aed007a17478a117a1862cfa55dd485c4c3b71-image.png" border={true} framed={true} />


## ERP master data ingestion

Your integration sends ERP master data to Paylocity for Finance using the ERP Integration APIs.

Supported master-data resources include:

- Accounts
- Currencies
- Employees
- Subsidiaries
- Tags and financial dimensions
- Vendors

Paylocity for Finance uses this data to:

- Apply the ERP's accounting structure to spend workflows
- Categorise transactions using the appropriate accounts and dimensions
- Associate activity with subsidiaries, employees, and vendors
- Support policy and approval workflows
- Generate accounting entries that can be posted back to the ERP

ERP reference identifiers preserve the relationship between records in the ERP and their corresponding records in Paylocity for Finance.

<Callout icon="ℹ️" theme="info">
  ### Synchronise dependencies first

  Some master-data resources refer to other ERP resources. For example, accounts, employees, tags, and vendors can be associated with subsidiaries. Follow the resource order described in [Connect an ERP](doc:onboard-erp) when completing the initial synchronisation.
</Callout>

## Accounting entry synchronisation

Paylocity for Finance generates accounting entries for supported financial activity, including card transactions, bills, bill payments, reimbursements, vendor credits, and other accounting events.

After an accounting entry is reviewed and made ready for synchronisation, your integration can:

1. Retrieve the ledger entry from Paylocity for Finance.
2. Create the corresponding accounting record in the ERP.
3. Return the ERP reference identifier and record URL.
4. Mark the entry as successfully synchronised or record a synchronisation error.

Ledger entries contain the accounting information required to reconstruct the financial impact in the ERP, including accounts, amounts, currencies, subsidiaries, vendors, employees, transaction dimensions, and line-level details.

Prepayment entries use a similar workflow and represent deferred or prepaid portions of a parent accounting entry.

## Synchronisation states

Accounting entries move through a synchronisation lifecycle.

| State           | Description                                                            |
| --------------- | ---------------------------------------------------------------------- |
| `sync_ready`    | The entry is available for retrieval and synchronisation with the ERP. |
| `sync_complete` | The entry has been successfully created or updated in the ERP.         |
| `sync_error`    | The ERP synchronisation failed and requires review or correction.      |

By default, the [Ledger Entries API](ref:ledger-entries) returns entries that are ready for synchronisation. After creating the corresponding ERP record, update the entry with the synchronisation outcome so that Paylocity for Finance can display its current state.

## Webhook-driven synchronisation

Your integration can subscribe to webhook events when ledger or prepayment entries become ready for synchronisation.

A webhook-driven workflow generally follows this sequence:

1. Paylocity for Finance sends a synchronisation-ready event.
2. Your endpoint verifies and accepts the webhook.
3. Your integration retrieves the complete accounting entry.
4. Your integration creates the corresponding record in the ERP.
5. Your integration updates Paylocity for Finance with the result.

Webhooks reduce the need to poll continuously for newly available entries. The webhook payload contains lightweight entry information, and the complete accounting record is retrieved through the corresponding<br />API.

For common webhook setup and security guidance, see:

- [Set up webhooks](doc:api-testing)
- [Webhook Security](doc:webhook-security)

For ERP-specific events and processing guidance, see [Set up ERP webhooks.](doc:setup-webhooks)

## Integration lifecycle

A typical ERP integration follows this lifecycle:

| Phase                           | Integration activity                                                                            |
| ------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Connect**                     | Establish API access and configure the ERP connection.                                          |
| **Synchronise master data**     | Send subsidiaries, currencies, accounts, tags, vendors, and employees to Paylocity for Finance. |
| **Configure accounting**        | Complete account mappings and related accounting settings in Paylocity for Finance.             |
| **Process spend**               | Use Paylocity for Finance for card, bill, reimbursement, and other supported spend workflows.   |
| **Retrieve accounting entries** | Retrieve ledger and prepayment entries that are ready for synchronisation.                      |
| **Post to the ERP**             | Create the corresponding accounting records in the ERP.                                         |
| **Return the result**           | Record the ERP identifier, ERP URL, and synchronisation status in Paylocity for Finance.        |
| **Maintain the integration**    | Continue refreshing master data and processing new accounting entries.                          |

The ERP Integration APIs also provide synchronisation sessions for coordinating the initial master-data push during onboarding. A synchronisation session indicates when the ERP has started and completed sending its entities so the Paylocity for Finance onboarding experience does not expose partially synchronised data.

## API groups

The ERP integration uses the following API groups:

### Master data

| API              | Purpose                                                                                 |
| ---------------- | --------------------------------------------------------------------------------------- |
| **Accounts**     | Synchronise the ERP chart of accounts.                                                  |
| **Currencies**   | Synchronise currencies used by ERP entities and accounting entries.                     |
| **Employees**    | Synchronise employees referenced by spend and accounting workflows.                     |
| **Subsidiaries** | Synchronise ERP legal entities and organisational hierarchies.                          |
| **Tags**         | Synchronise financial dimensions such as departments, locations, classes, and projects. |
| **Vendors**      | Synchronise ERP vendors used in accounting workflows.                                   |

### Accounting synchronisation

| API                    | Purpose                                                                         |
| ---------------------- | ------------------------------------------------------------------------------- |
| **Ledger Entries**     | Retrieve accounting entries and return ERP synchronisation results.             |
| **Prepayment Entries** | Retrieve and update prepayment or amortisation entries.                         |
| **Sync Sessions**      | Coordinate the initial ERP master-data synchronisation during onboarding.       |
| **Webhooks**           | Notify the integration when supported entries become ready for synchronisation. |

Refer to the [ERP Integration API Reference](ref:ledger-entries) for supported operations, request fields, response schemas, validation rules, and errors.

## Implementation considerations

### Preserve ERP reference identifiers

Use stable ERP reference identifiers when synchronising master data. These identifiers allow Paylocity for Finance and the ERP to maintain the relationship between corresponding records.

### Keep master data current

Refresh ERP master data regularly so that new or updated accounts, dimensions, employees, subsidiaries, and vendors are available to Paylocity for Finance workflows.

### Make entry processing idempotent

A ledger entry or webhook notification might be retrieved or received more than once. Ensure that retrying the integration does not create a duplicate ERP accounting record.

### Return synchronisation outcomes

After processing an entry, return the result to Paylocity for Finance. For failed entries, provide a useful error description so that the finance team can investigate and make the entry ready for<br />synchronisation again.

### Process prepayments in dependency order

When a prepayment entry is associated with a parent ledger entry, synchronise the parent accounting entry before its related prepayment entries.

## Continue building

- [Connect an ERP](doc:onboard-erp) to implement the initial connection and master-data synchronisation.
- [Sync Transactions](doc:process-transactions) to retrieve ledger and prepayment entries and return their ERP results.
- [Set up ERP webhooks](doc:setup-webhooks) to initiate synchronisation using event notifications.
- Browse the [**ERP Integration API Reference**](ref:ledger-entries) for operation-level documentation.
