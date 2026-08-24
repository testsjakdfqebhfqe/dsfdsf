---
api:
  file: control-d.json
  operationId: get_devices
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 🚧 Organization Accounts
>
> If you have a organization account (ignore this if you do not), you can "impersonate" an admin of a child sub-organization, by supplying `X-Force-Org-Id: org_id_goes_here` HTTP header along with all API calls within the Profiles scope. This will allow you to view, create and modify Devices within the target sub-organization using the API token of the parent (main) Organization.
>
> Additionally, to retrieve only User type devices, append `/users` to this API call, or `/routers` to retrieve only Router type devices.

<br />

> ❗️ Changes in the works
>
> We’re currently updating this API to streamline behavior and improve query performance. As part of this change, the `last_activity` and `clients` fields will be removed from the response soon. In the meantime, if you still need these two fields, please include the query parameter `last_activity=1` in your requests.