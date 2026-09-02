---
title: Webhook Security
excerpt: >-
  Verify webhook payloads using HMAC-SHA256 and protect webhook endpoints and
  secret keys.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Webhook security

Paylocity for Finance sends webhook payloads over `HTTPS` and signs each payload using `HMAC-SHA256`. Verify the signature before trusting the payload or initiating a downstream action.

<Callout icon="⚠️" theme="warn">
  ### Verify before processing

  Do not create ERP records, complete procurement actions, send notifications, or perform other trusted operations until the webhook signature has been verified.
</Callout>

## How webhook signatures work

When Paylocity for Finance sends a webhook, it calculates an HMAC-SHA256 signature using:

- The webhook payload
- The HMAC secret key generated for the webhook

The signature is included in the following request header:

```http
X-Airbase-Hmac-Sha256: <signature>
```

Your receiving application calculates a signature from the incoming payload using the same HMAC key. If the calculated signature matches the signature in the request header, the payload has passed verification.

HMAC verification helps confirm:

- **Integrity:** The webhook payload has not been modified since it was signed.
- **Authenticity:** The request was signed using the HMAC key configured for the webhook.

## Obtain the HMAC key

The HMAC key is displayed after you create a webhook in Paylocity for Finance. Copy and store the key securely when it is displayed. The key cannot be recovered after you leave the webhook creation window. For the webhook creation and HMAC key retrieval process, see [Set up webhooks.](doc:api-testing)

> ### Protect the HMAC key
>
> Treat the HMAC key as a secret. Do not include it in source code, client-side applications, screenshots, logs, shared API-client requests, or support messages.
>

## Verify a webhook signature

Perform signature verification before parsing or acting on the webhook payload:

1. Read the raw HTTP request body.
2. Read the signature from the X-Airbase-Hmac-Sha256 header.
3. Calculate an HMAC-SHA256 signature from the raw request body using the webhook's HMAC key.
4. Compare the calculated signature with the received signature using a constant-time comparison.
5. Reject the request if the signature is missing or does not match.
6. Parse and process the JSON only after verification succeeds.

> **Use the raw request body**
>
> Verify the signature against the unmodified request body exactly as it was received. Parsing and serialising JSON can change whitespace, property order, or character encoding and cause signature verification to fail.

## Python example

The following example calculates an HMAC-SHA256 signature from the raw request body and compares it with the signature received in the webhook header.

```python
import hmac
import hashlib
import json

def verify_webhook_signature(secret_key, request):
		# Get the signature from POST request header
    signature = request.headers.get('X-Airbase-Hmac-Sha256')

    # Encode the secret key
    encoded_secret_key = secret_key.encode("utf-8")
    
    # Create the HMAC object using the secret key and SHA256 algorithm
    hmac_obj = hmac.new(encoded_secret_key, request.body, digestmod=hashlib.sha256)

    # Generate the HMAC digest
    generated_signature = hmac_obj.hexdigest()

    # Compare the generated HMAC digest with the received signature
    return hmac.compare_digest(generated_signature, signature)
```

If `verify_webhook_signature` returns `True`, the locally calculated signature matches the signature supplied with the webhook request.

> ### Signature format
>
> This example expects the value in X-Airbase-Hmac-Sha256 to be a hexadecimal HMAC-SHA256 digest calculated from the raw request body. Ensure that your implementation uses the signature format documented for Paylocity for Finance webhooks.

## Handle verification failures

If the signature is missing or invalid:

- Return a non-2xx response.
- Do not trust or process the payload.
- Do not perform the associated downstream action.
- Do not include the calculated signature or HMAC key in the response.
- Record only the diagnostic information required for investigation.

Repeated verification failures can indicate:

- An incorrect HMAC key
- A key associated with a different webhook
- Test and production configurations being mixed
- Modification of the request body before verification
- An incorrect signature encoding
- Requests from an untrusted source

## Protect against duplicate processing

Signature verification confirms the integrity of a delivery, but the same valid event might be delivered more than once.&#x20;

Use the event identifier to detect duplicate deliveries. Make downstream processing idempotent so that receiving the same event again does not duplicate an ERP record, procurement action, notification, or other operation.

## Store keys securely

Store HMAC keys in a server-side secret-management system or protected environment configuration. Use separate HMAC keys for:

- Test and production environments
- Different receiving applications
- Destinations with different security boundaries

Limit access to the services and personnel that require the key for webhook verification.

<br />
