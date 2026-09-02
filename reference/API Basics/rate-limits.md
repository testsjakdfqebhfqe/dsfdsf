---
title: Rate Limits
excerpt: >-
  Understand and manage rate limits when integrating with Paylocity for Finance
  APIs.
deprecated: false
hidden: false
metadata:
  robots: index
---
<Callout icon="ℹ️" theme="info">
  #### _Paylocity for Finance APIs support a maximum of 500 requests per minute per company. This limit is shared across all Paylocity for Finance API endpoints for the company._
</Callout>

# Overview

Rate limits help maintain the availability, stability, and performance of Paylocity for Finance APIs. They prevent a single integration from consuming excessive capacity and help ensure consistent service for all customers and partners. If requests for a company exceed the permitted rate, the API returns an HTTP status code `429 Too Many Requests`. A `429 Too Many Requests` response indicates that the company has exceeded the permitted request volume for the current rate-limit window.

# How the rate limit is applied

The following limit applies consistently across Paylocity for Finance APIs:

| Scope                | Limit                                   |
| -------------------- | --------------------------------------- |
| Per company          | 500 requests per minute                 |
| Applicable endpoints | All Paylocity for Finance API endpoints |

The limit is applied at the company level, not separately to each endpoint. Requests made by different integrations or API tokens for the same company may therefore contribute to the same company-level limit.

> **_Note:&#x20;_**_If multiple applications, services, or scheduled jobs access Paylocity for Finance APIs for the same company, coordinate their request volume so that their combined traffic remains within 500 requests per minute._

# Prevent rate limit errors

Design your integration to control request volume before requests are sent.

## Reduce unnecessary requests

- Cache data that does not need to be retrieved repeatedly.
- Avoid duplicate requests for the same resource.
- Request only the data required by the integration.
- Avoid polling more frequently than the business workflow requires.
- Reuse previously retrieved identifiers, such as`subsidiary_id`, when appropriate.

## Use pagination efficiently

For paginated endpoints:

- Select a page_size appropriate for the volume of data being retrieved.
- Retrieve the next page only when pagination.next is not null.
- Avoid restarting pagination from the first page unless the complete data set must be refreshed.
- Avoid requesting pages concurrently if doing so could exceed the company-level rate limit.

## Throttle requests on the client

Implement client-side throttling to keep the combined request rate below the allowed limit.<br />Common approaches include:

- Token bucket
- Leaky bucket
- Fixed request queue
- Centralised throttling shared by application workers

When several workers, services, or jobs make requests for the same company, use a shared limiter rather than an independent limiter in each process.

# Handle 429 Too Many Requests

When the API returns 429 Too Many Requests:

1. Stop sending additional requests for the affected company.
2. Delay the failed request.
3. Retry using exponential backoff.
4. Add random jitter to prevent multiple workers from retrying simultaneously.
5. Limit the number of retries.
6. Record the response in application logs and monitoring.
7. Surface a controlled integration error if retries are exhausted.

> **_Retry guidance:_**_<br />Retry only requests that failed with 429 Too Many Requests. Do not repeat requests that have already completed successfully._

# Monitoring recommendations

Monitor API usage by company and track:

- Requests per minute
- Number of 429 responses
- Retry attempts
- Retry success rate
- Requests by endpoint
- Requests by application or worker
- Queue depth and processing delay

Consider alerting before usage reaches the maximum rate so the integration can reduce traffic proactively.

<br />
