---
title: Organization
excerpt: These endpoints allow you to manage your business account.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
> 📘 Sub-Organization Impersonation
>
> if you create sub-organizations, your main organization's API key can be used to manage all child sub-organizations and all their assets. In order to "impersonate" an admin of a child sub-organization, supply `X-Force-Org-Id: org_id_goes_here` header for every request that is relevant to that sub-organization (while managing their Devices, Profiles, etc).
