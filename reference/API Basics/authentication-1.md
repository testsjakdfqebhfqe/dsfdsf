---
title: Authentication
excerpt: >-
  Understand how to authenticate requests to Paylocity for Finance APIs using an
  access token.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Paylocity for Finance APIs use token-based authentication. Every API request must include a valid access token in the HTTP Authorization request header.

The required header format is: `Authorization: Token {access_token}`

> **_Important:_**<br />_Include the literal prefix Token, followed by a space, before the access token. Requests with a missing, invalid, or incorrectly formatted token will not be authenticated._

If you do not have an access token, follow the [Quickstart guide](doc:quickstart) to generate one and make your first API request.

# Base URL

Send API requests to the following base URL: [https://api.airbase.io](https://api.airbase.io "https://api.airbase.io")

Combine the base URL with the versioned path for the resource you want to access. For example:

[https://api.airbase.io/v1/subsidiaries/](https://api.airbase.io/v1/subsidiaries/ "https://api.airbase.io/v1/subsidiaries/")

# Required Headers

Include the following headers with each request:

```http
Accept: application/json
Authorization: Token {access_token}
```

| Header          | Required | Description                                                                                                       |
| --------------- | -------- | ----------------------------------------------------------------------------------------------------------------- |
| `Authorization` | Yes      | Provides the access token used to authenticate the request. The value must use the format `Token {access_token}`. |
| `Accept`        | Yes      | Indicates that the client expects the response in JSON format. Use `application/json`.                            |

# How authentication works

Paylocity for Finance APIs are REST APIs accessed over HTTPS. Your application sends an HTTP request to an API endpoint and includes its access token in the Authorization header. For example:

```curl
curl --location 'https://api-stage.airbase.io//v1/subsidiaries/' \
--header 'Accept: application/json' \
--header 'Authorization: Token {access_token}'
```

The API validates the token before processing the request:

1. Your application sends an HTTPS request.
2. The request includes the access token in the Authorization header.
3. The API validates the token and determines the company the token can access.
4. If the token is valid, the API processes the request.
5. If the token is missing or invalid, the API returns 401 Unauthorized.

# 401 Unauthorized

The API returns 401 Unauthorized when authentication fails or when the access token is missing or invalid.

Example:

```json
{
  "error_code": 407107,
  "error_message": "unauthorized"
}
```

# Common causes

A 401 Unauthorized response can occur when:

- The Authorization header is missing.
- The access token is missing or invalid.
- The Token prefix is missing.
- Bearer is used instead of Token.
- There is no space between Token and the access token.
- The token was copied incorrectly.
- The application is using an incorrect or empty environment variable.
- The Token has expired.

# Troubleshooting

Verify that the request contains a correctly formatted header:

`Authorization: Token {access_token}`&#x20;

Check the following:

- The header name is Authorization.
- The header value begins with the literal word Token.
- A space separates Token from the access token.
- The access token does not include quotation marks.
- The access token does not contain unintended leading or trailing spaces.
- The request is sent to the correct base URL.
- The token value has not been replaced by an unresolved variable or placeholder.

# Token Expiry

An expiry date is specified when an access token is generated. Integrations should record that date and replace the token before it expires.

<br />
