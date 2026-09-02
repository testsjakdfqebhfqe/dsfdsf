---
title: API Versioning
excerpt: >-
  Understand how Paylocity for Finance API versions are identified and how
  changes are communicated.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Paylocity for Finance APIs use versioning to introduce changes while helping integrations remain stable and predictable.&#x20;

The API version is included in the request URL:

`https://api.airbase.io/v1/{resource}/`

For example: Company Subsidiaries API

`https://api.airbase.io/v1/subsidiaries/`

# Versioning strategy

Paylocity for Finance uses URL-based versioning. The major version appears in the URL immediately before the resource:

`v1/subsidiaries/`&#x20;

A new major version may be introduced when a change is not backward compatible with the existing version. Examples of potentially breaking changes include:

- Removing or renaming a response field
- Changing a field’s data type
- Making an optional parameter required
- Changing the meaning or format of an existing value
- Removing an endpoint
- Changing authentication requirements
- Changing established response behaviour

Backward-compatible improvements may be introduced without changing the major API version. These may include:

- Adding an optional request parameter
- Adding a new endpoint
- Adding a new optional response field
- Adding a new supported filter or enum value
- Correcting documentation without changing API behaviour

> **_Important:<br />_**_Integrations should ignore unknown response fields unless the documentation explicitly requires strict schema validation. New fields may be added to existing responses as the API evolves._

# Deprecation and retirement

When an API version or endpoint is scheduled for deprecation, Paylocity will communicate:

- The affected version or endpoint
- The deprecation date
- The planned retirement date
- The recommended replacement, when available
- Any migration actions required from API consumers

Deprecated APIs may remain accessible during the communicated migration period, but should not be used for new integrations.

After retirement, the affected API version or endpoint may no longer be available.
