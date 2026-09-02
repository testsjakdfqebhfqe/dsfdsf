---
title: Errors
excerpt: >-
  Understand the standard HTTP status codes and error response format used by
  the Paylocity for Finance APIs.
deprecated: false
hidden: false
metadata:
  robots: index
---
Paylocity for Finance APIs use standard HTTP status codes to indicate whether a request succeeded or failed.<br /><br />Error responses generally include a machine-readable error_code and a human-readable error_message. Validation errors may also include a data object containing field-level details.

## Error Response

```json
{
  "error_code": 400100,
  "error_message": "Invalid request",
  "data": {
    "year": [
      "This field is required."
    ],
    "month": [
      "This field is required."
    ]
  }
}
```

## Response Fields

| Field           | Type             | Description                                                                                            |
| --------------- | ---------------- | ------------------------------------------------------------------------------------------------------ |
| `error_code`    | integer          | A machine-readable error identifier.                                                                   |
| `error_message` | string           | A human-readable summary of the error.                                                                 |
| `data`          | object or `null` | Additional context about the error. For validation errors, this may contain messages grouped by field. |

Not every error response includes data. Some responses, including rate-limit responses, may have an empty body.

## HTTP Status Codes

| Status                      | Description                                                                                                           |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `400 Bad Request`           | The request is invalid or is missing a required parameter. Review the response body and correct the indicated fields. |
| `401 Unauthorized`          | The authentication token is missing or invalid. Provide a valid token in the `Authorization` header.                  |
| `403 Forbidden`             | The credentials are valid, but the authenticated company does not have access to the requested API or resource.       |
| `404 Not Found`             | The requested resource does not exist or is not accessible to the authenticated company.                              |
| `405 Method Not Allowed`    | The endpoint does not support the requested HTTP method.                                                              |
| `429 Too Many Requests`     | The request rate limit has been exceeded. Retry the request after reducing request frequency.                         |
| `500 Internal Server Error` | An unexpected server error prevented the request from being completed.                                                |
| `503 Service Unavailable`   | The service is temporarily unavailable.                                                                               |

## Support

For assistance with Finance API errors, contact: [ab-api@paylocity.com.](mailto:ab-api@paylocity.com) Include the endpoint, HTTP method, status code, error code, approximate request timestamp, environment, and any available request or correlation ID. Do not include access tokens, client secrets, bank-account details, card details, or other sensitive information.

<br />
