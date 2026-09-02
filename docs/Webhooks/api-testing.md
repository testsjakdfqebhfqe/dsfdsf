---
title: Set up webhooks
excerpt: >-
  Create a webhook and configure an endpoint to receive Paylocity for Finance
  events.
---
Webhooks send notifications to your application when supported activity occurs in Paylocity for Finance. Use webhooks to initiate downstream workflows without continuously polling the API.

<Callout icon="ℹ️" theme="info">
  ### Event availability

  Available events depend on the Paylocity for Finance capabilities enabled for your company.

  Refer to the applicable use-case Guide or API Reference documentation for supported events, triggers, and payloads.
</Callout>

## How webhooks work

When a supported event occurs:

1. Paylocity for Finance sends an HTTP `POST` request to the configured
   destination URL.
2. Your endpoint verifies the payload signature.
3. Your endpoint validates and records the event.
4. Your endpoint returns a successful `2xx` response.
5. Your application completes the downstream workflow.

A webhook can contain identifiers rather than the complete resource. Refer to the applicable event documentation for the confirmed payload.

## 1. Prepare your endpoint

Create an endpoint that can receive webhook deliveries.

The endpoint must:

- Be publicly accessible over HTTPS
- Accept HTTP `POST` requests
- Accept JSON request bodies
- Preserve the raw request body for signature verification
- Return a `2xx` response after accepting a valid delivery
- Handle duplicate deliveries without repeating a downstream action

<Callout icon="⚠️" theme="warn">
  ### Respond promptly

  Validate and record the event, then return a successful response. Process longer-running downstream workflows separately to avoid delivery timeouts.
</Callout>

## 2. Create a webhook

An administrator can create a webhook in Paylocity for Finance.

1. Go to Dashboard> Settings > Connections > Tokens and Webhooks > Webhooks.

   ![](https://files.readme.io/e203a08e4573bd933cc0aabcc1bf240f50f188082f1cbb298956a61a92374d47-image.png)
2. Add the details on the Create Webhook pop-up. Give the webhook a name and enter the Webhook POST URL, the endpoint where notifications will be sent. You can set this up as a listening service on an automation tool like Zapier or Workato, or create one on a custom server.

   ![](https://files.readme.io/ec52772988c96ce1631ce4568fb20fe5d9d1853be0675ea22b9f3626a2e66ded-image.png)
3. Submit the webhook configuration.
4. Copy the HMAC secret key displayed after the webhook is created.

   ![](https://files.readme.io/abd8d970f97963e431294fc1f1e78a0e59c84cfd5ef6379f7007caec912f07d0-image.png)

<Callout icon="⚠️" theme="warn">
  ### Save the HMAC key

  Copy and store the HMAC secret key securely when it is displayed. The key cannot be recovered after you leave the window.

  Your application uses this key to verify that webhook deliveries were sent by Paylocity for Finance and were not modified in transit.
</Callout>

For signature verification instructions, see [Webhook Security](doc:webhook-security).

## 3. Select events

Subscribe only to the events required by the integration.

Selecting only the required events:

- Reduces unnecessary delivery traffic
- Simplifies event routing
- Limits the data received by the application
- Makes monitoring and troubleshooting easier

Event names, triggers, and payloads vary by use case. Refer to:

- [Set up ERP webhooks](doc:setup-webhooks)
- [Set up Guided Procurement webhooks](doc:guided-procurement-webhooks)

## 4. Accept a delivery

For each delivery:

1. Read the raw request body.
2. Verify the signature in the `X-Airbase-Hmac-Sha256` header.
3. Validate the event type and required fields.
4. Check whether the event has already been accepted.
5. Store the event or add it to a processing queue.
6. Return a `2xx` response.

Do not perform trusted downstream actions unless signature verification succeeds.

## Handle duplicate deliveries

Your endpoint might receive the same event more than once. Make webhook processing idempotent so that a repeated delivery does not duplicate an ERP record, procurement action, notification, or other downstream operation.

When the payload provides an event identifier:

1. Check whether the identifier has already been recorded.
2. If it has, acknowledge the delivery without repeating the action.
3. If it has not, accept and record the event.
4. Process the associated action once.

## Troubleshooting

### The webhook is not received

Check that:

- The destination URL is correct.
- The endpoint is publicly accessible over HTTPS.
- The webhook is enabled.
- The required event is selected.
- The endpoint accepts HTTP `POST` requests.
- The endpoint accepts JSON request bodies.
- Network and firewall rules allow the delivery.
- The webhook is configured for the correct company and environment.

### The delivery times out

Store or enqueue the event and return a `2xx` response before starting
long-running processing.

### The event is processed more than once

Use the event identifier to detect duplicate deliveries and make the
downstream operation safe to repeat.

### Signature verification fails

Confirm that:

- The correct HMAC key is being used.
- The key belongs to the webhook sending the delivery.
- The test and production keys have not been interchanged.
- Verification uses the raw request body.
- The signature is read from `X-Airbase-Hmac-Sha256`.
- Middleware has not modified the request body before verification.

For detailed verification guidance, see [Webhook Security](doc:webhook-security)

<br />
