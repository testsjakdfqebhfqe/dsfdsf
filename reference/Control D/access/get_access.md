---
api:
  file: control-d.json
  operationId: get_access
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This endpoint returns a list of logged or authorized IPs on a specific device.

<br />

> 🚧 Organization Accounts
>
> If you have a organization account (ignore this if you do not), you can "impersonate" an admin of a child sub-organization, by supplying `X-Force-Org-Id: org_id_goes_here` HTTP header along with all API calls within this scope. This will allow you to view, and modify access IPs within the target sub-organization using the API token of the parent (main) Organization.