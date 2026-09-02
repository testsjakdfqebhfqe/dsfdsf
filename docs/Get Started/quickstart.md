---
title: Quickstart
excerpt: >-
  Generate an API token and make your first authenticated request to Paylocity
  for Finance.
deprecated: false
hidden: false
metadata:
  robots: index
---
This Quickstart guide walks you through the essential steps required to prepare your environment and make your first API call. It outlines how to obtain access, generate authentication credentials, and configure your API client so you can begin using PCTY for Finance endpoints immediately. You'll create an access token and call the [Company Subsidiaries](ref:company-subsidiaries) to retrieve a list of subsidiaries in the authenticated company.

<Callout icon="ℹ️" theme="info">
  ### Access Required

  Complete the access requirements in the [Paylocity for Finance APIs overview](doc:paylocity-for-finance-overview) before starting this Quickstart. This example requires access to the Financial Reporting APIs.
</Callout>

# Step 1: Generate an access token

PCTY for Finance uses token-based authentication. Every request must include an Authorization header containing a valid API token.

1. As an **Admin**, navigate to **Settings > Connections > Tokens & Webhooks**.


<Image src="https://files.readme.io/85a6964a7b4e80d903a591b20c866666e4ef5714cb503e71b38a6d7470be8041-Picture1.png" width="-2px" framed={true} />


2. Click **Generate Access Token&#x20;**&#x61;nd provide an appropriate **Access Token Name** and **Expiry Date**.


   <Image src="https://files.readme.io/2f8b95147c5c81dcdf6429b76dacdc4d9a9d01e5076379ec2c05ef88d2ab37d4-image.png" align="center" framed={true} />


3. Click **Generate** and copy the token immediately. Store the token securely, as you cannot view it again after leaving the screen.


   <Image src="https://files.readme.io/efd2ee95f8ab4bcba165a2cebdca045583877b96318913f49a18d9c381aec7af-image.png" align="center" framed={true} />


<Callout icon="⚠️" theme="info">
  ### Important

  Copy the token immediately and store it securely. The token cannot be viewed again after you leave the page.
</Callout>

# Step 2: Make your first request

Send a `GET` request to retrieve the company subsidiaries available to your Paylocity for Finance account. Use the following values:

| Setting        | Value                    |
| -------------- | ------------------------ |
| Base URL       | `https://api.airbase.io` |
| Endpoint       | `/v1/subsidiaries/`      |
| Method         | `GET`                    |
| Authentication | API Key                  |
| Accept header  | `application/json`       |

Requests use token authentication in the Authorization header.

Replace `<your_access_token>` with the token generated in the previous step. Include the literal Token prefix followed by one space.

```curl
curl --location 'https://api.airbase.io/v1/subsidiaries/' \
--header 'Accept: application/json' \
--header 'Authorization: Token <your_access_token>'
```

# Step 3: Verify the response

A successful request returns `200 OK` and a paginated list of company subsidiaries.

```json
{
  "data": [
    {
      "id": "019750a2-1a2b-7cde-f012-345678901234",
      "name": "Acme Corp US",
      "display_name": "Acme US",
      "description": "United States headquarters",
      "is_default": true,
      "parent_subsidiary_id": null,
      "country": {
        "name": "United States",
        "alpha_2_code": "US",
        "alpha_3_code": "USA"
      },
      "currency": {
        "iso_code": "USD",
        "symbol": "$"
      },
      "address": {
        "address1": "123 Market St",
        "address2": null,
        "city": "San Francisco",
        "state": "CA",
        "zip_code": "94105",
        "country": "US"
      },
      "gl_sync_enabled": true,
      "gl_subsidiary": {
        "erp_reference_id": "1",
        "name": "Acme Corp US",
        "provider": "netsuite"
      },
      "created_at": "2025-01-15T10:30:00Z",
      "updated_at": "2025-01-15T10:30:00Z"
    },
    {
      "id": "019750a2-2c3d-7ef0-1234-567890abcdef",
      "name": "Acme Corp UK",
      "display_name": "Acme UK",
      "description": "United Kingdom subsidiary",
      "is_default": false,
      "parent_subsidiary_id": "019750a2-1a2b-7cde-f012-345678901234",
      "country": {
        "name": "United Kingdom",
        "alpha_2_code": "GB",
        "alpha_3_code": "GBR"
      },
      "currency": {
        "iso_code": "GBP",
        "symbol": "£"
      },
      "address": {
        "address1": null,
        "address2": null,
        "city": null,
        "state": null,
        "zip_code": null,
        "country": "GB"
      },
      "gl_sync_enabled": false,
      "gl_subsidiary": null,
      "created_at": "2025-01-16T09:00:00Z",
      "updated_at": "2025-01-16T09:00:00Z"
    }
  ],
  "pagination": {
    "next": null,
    "previous": null,
    "page": 1,
    "page_size": 250
  }
}
```

# Troubleshoot your first request

### 401 Unauthorized

The token is missing, invalid, expired, or formatted incorrectly. Check that:

- The request includes an Authorization header.
- The value begins with the literal Token prefix.
- There is one space between Token and the token value.
- The token belongs to the environment receiving the request.
- The complete token was copied without quotation marks or extra spaces.

### 403 Forbidden

The token is valid, but the authenticated company does not have access to the requested API or resource. Confirm that Financial Reporting API access is enabled for the company. API-family availability and enablement requirements are described in the [Paylocity for Finance APIs overview](doc:paylocity-for-finance-overview).

# Continue building

After the first request succeeds, continue with the documentation for your integration goal:

[ERP Integration](doc:erp-integration-overview): Synchronise ERP master data, retrieve accounting entries, and return synchronisation outcomes.

[Financial Reporting](doc:financial-reporting-overview): Retrieve financial records for reporting, reconciliation, audit, and analytics.<br />Guided Procurement: Connect procurement requests, milestones, files, and approval workflows.

Refer to the [API Reference](ref:authentication-1) for operation-specific parameters, request bodies, response schemas, and errors.

<br />
