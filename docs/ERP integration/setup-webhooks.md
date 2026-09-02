---
title: Set up ERP webhooks
excerpt: >-
  Use webhooks to receive real-time notifications when ledger entries are ready
  to sync to your ERP. This document explains how to use webhooks to receive
  real-time notifications when ledger entries are ready to be synced to your ERP
  system. 
---
## Overview

Paylocity for finance provides webhook notifications to inform your systems when ledger entries transition to a "sync ready" state. This allows you to:

- Automatically trigger ERP sync workflows when entries are ready
- Build real-time integrations without polling the API
- Reduce latency between Paylocity for finance and your ERP system

### When Do Webhooks Fire?

The ledger entry sync ready webhook fires when entries move to the `sync_ready` state **from within the Paylocity for finance platform**. This includes:

- ✅ Transactions that complete settlement and are ready for export
- ✅ Bills that are approved and ready for sync
- ✅ Reimbursements that are approved and ready for sync
- ✅ Entries marked as sync ready via the dashboard
- ✅ Prepayment/amortization entries that are generated and ready for sync

The webhook does **not** fire when:

- ❌ Status is updated via the Public API (to prevent circular notifications)
- ❌ Entries are already in `sync_ready` state (no duplicate notifications)

***

## Available Events

| Event Name                  | Event Key                     | Description                                                         |
| --------------------------- | ----------------------------- | ------------------------------------------------------------------- |
| Ledger Entry Sync Ready     | `ledger.entry.sync.ready`     | Fired when one or more ledger entries are ready to be synced to ERP |
| Prepayment Entry Sync Ready | `prepayment.entry.sync.ready` | Fired when one or more ledger entries are ready to be synced to ERP |

***

### Step 1: Navigate to Webhook Settings

1. Log in to your Paylocity for finance account
2. Go to **Settings** → **Tokens & Webhooks** or navigate directly to:
   - Production: `https://dashboard.airbase.io/settings/tokens-webhooks/tokens`
   - Staging: `https://stage.airbase.io/settings/tokens-webhooks/tokens`&#x20;
3. Click **Add Webhook**

### Step 2: Configure the Webhook

| Field                 | Description                                                             |
| --------------------- | ----------------------------------------------------------------------- |
| **URL**               | The HTTPS endpoint where Paylocity for finance will send webhook events |
| **Events**            | Select `ledger.entry.sync.ready` from the available events              |
| **Secret** (optional) | A shared secret used to verify webhook signatures                       |

### Step 3: Prepare Your Endpoint

<Callout theme="warning">
  ### Important:

  Your webhook endpoint must be a publicly accessible URL that accepts unauthenticated `POST` requests. Paylocity for finance will send webhook payloads directly to this endpoint without any authentication headers (other than the optional signature for verification).
</Callout>

### Ensure your endpoint:

- Is publicly accessible (open endpoint)
- Accepts `POST` requests without authentication
- Returns a `2xx` status code within 30 seconds
- Handles JSON payloads with `Content-Type: application/json`

***

## Event: Ledger Entry Sync Ready

This event notifies you when ledger entries are ready to be synced to your ERP system.

### Event Details

| Property       | Value                     |
| -------------- | ------------------------- |
| Event Key      | `ledger.entry.sync.ready` |
| HTTP Method    | `POST`                    |
| Content Type   | `application/json`        |
| Payload Format | Bulk (array of entries)   |

### Payload Structure

```json
{
  "id": "f42560e6-f2e2-4330-9352-cfc0aacb37f5",
  "object": "event",
  "type": "ledger.entry.sync.ready",
  "created_date": "2026-02-27T08:18:11.260707",
  "data": {
    "entries": [
      {
        "id": "01f01a92-96f3-4b0a-97e1-920c44c72101",
        "airbase_id": "01f01a92-96f3-4b0a-97e1-920c44c72101",
        "state": "sync_ready",
        "type": "bill",
        "created_date": "2026-02-27T08:18:11.067586",
        "updated_date": "2026-02-27T08:18:11.067575"
      }
    ]
  }
}
```

***

## Payload Reference

### Entry Object

Each entry in the `entries` array contains the following fields:

| Field          | Type     | Description                                                                                                                                                                             |
| -------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`           | UUID     | Unique identifier for the ledger sync operation. Use this ID to fetch full details via the [Ledger Entries API](https://developer.paylocity.com/finance/reference/list-ledger-entries). |
| `airbase_id`   | UUID     | **Deprecated** — legacy alias for `id`. Still emitted in every payload during the partner migration window and will be removed in a future release. Prefer `id`.                        |
| `state`        | string   | Current state of the entry (always `sync_ready` for this event)                                                                                                                         |
| `type`         | string   | Type of ledger entry                                                                                                                                                                    |
| `created_date` | ISO 8601 | Timestamp when the sync operation was created                                                                                                                                           |
| `updated_date` | ISO 8601 | Timestamp when the sync operation was last updated                                                                                                                                      |

## Use Cases

### Real-Time ERP Sync

Automatically sync ledger entries to your ERP when they become ready:

```python
@app.route('/webhooks/paylocity-for-finance', methods=['POST'])
def handle_webhook():
    event = request.json
    if event['event'] == 'ledger.entry.sync.ready':
        for entry in event['data']['entries']:
            # Fetch full entry details from API
            entry_details = api.get_ledger_entry(entry['id'])
            # Sync to your ERP
            erp.create_journal_entry(entry_details)
            # Mark as synced in Paylocity for finance
            api.update_ledger_entry(
                entry['id'],
                state='sync_complete'
            )
    return '', 200
```

### Notification System

Send alerts to your finance team when entries are ready for review:

```python
@app.route('/webhooks/paylocity-for-finance', methods=['POST'])
def handle_webhook():
    event = request.json
    if event['event'] == 'ledger.entry.sync.ready':
        entry_count = len(event['data']['entries'])
        slack.send_message(
            channel='#finance',
            text=f'📊 {entry_count} ledger entries are ready for ERP sync'
        )
    return '', 200
```

### Batch Processing Queue

Queue entries for batch processing during off-peak hours:

```python
@app.route('/webhooks/paylocity-for-finance', methods=['POST'])
def handle_webhook():
    event = request.json
    if event['event'] == 'ledger.entry.sync.ready':
        for entry in event['data']['entries']:
            # Add to processing queue
            job_queue.enqueue(
                'sync_to_erp',
                id=entry['id'],
                entry_type=entry['type']
            )
    return '', 200
```

***

## Best Practices

### Respond Quickly

Return a `2xx` response as soon as you receive the webhook. Process the data asynchronously to avoid timeouts.

```python
@app.route('/webhooks/paylocity-for-finance', methods=['POST'])
def handle_webhook():
    # Acknowledge receipt immediately
    event = request.json
    # Process asynchronously
    background_task.delay(event)
    return '', 200  # Return quickly
```

### Handle Duplicates

While rare, webhooks may occasionally be delivered more than once. Ensure your processing is idempotent:

```python
def process_entry(entry):
    # Check if already processed
    if redis.exists(f"processed:{entry['id']}"):
        return  # Skip duplicate
    # Process the entry
    sync_to_erp(entry)
    # Mark as processed (with TTL)
    redis.setex(f"processed:{entry['id']}", 86400, '1')
```

### Verify Webhook Signatures

If you configured a webhook secret, verify the signature to ensure the request is from Paylocity for finance:

```python
import hmac
import hashlib

def verify_signature(payload, signature, secret):
    expected = hmac.new(
        secret.encode(),
        payload.encode(),
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(expected, signature)

@app.route('/webhooks/paylocity-for-finance', methods=['POST'])
def handle_webhook():
    signature = request.headers.get('x-airbase-hmac-sha256')
    if not verify_signature(request.data.decode(), signature, WEBHOOK_SECRET):
        return 'Invalid signature', 401
    # Process webhook...
```

### Implement Retry Logic

If your initial processing fails, implement retry logic with exponential backoff:

```python
@celery.task(bind=True, max_retries=5)
def sync_to_erp(self, entry):
    try:
        erp.create_journal_entry(entry)
    except ERPConnectionError as e:
        # Retry with exponential backoff
        raise self.retry(exc=e, countdown=2 ** self.request.retries)
```

### Monitor Webhook Health

Set up monitoring to detect issues with webhook delivery:

- Track response times and error rates
- Alert on repeated failures
- Log all webhook events for debugging

***

## Troubleshooting

### Webhook Not Received

1. Verify your endpoint URL is correct and publicly accessible
2. Check that the `ledger.entry.sync.ready` event is enabled
3. Ensure your endpoint accepts `POST` requests with JSON content
4. Check firewall rules allow traffic from Paylocity for finance IPs

### Duplicate Webhooks

Implement idempotency using the `id` field as described in [Handle Duplicates](#handle-duplicates).

### Missing Entry Details

The webhook payload contains minimal information by design. Use the `id` to fetch complete entry details:

```bash
curl -X GET "https://api.airbase.io/public/v1/accounting/ledger-entries/{id}" \
  -H "Authorization: Token <your_api_token>"
```

***

## Related Documentation

- [Ledger Entries API](https://developer.paylocity.com/finance/reference/list-ledger-entries) — Full API reference for ledger entries
- [GL Accounts API](https://developer.paylocity.com/finance/reference/list-accounts) — Managing GL accounts
- [Subsidiaries API](https://developer.paylocity.com/finance/reference/list-subsidiaries) — Managing subsidiaries

<br />