---
api:
  file: control-d.json
  operationId: get_profiles
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Each Profile has a primary key (`PK` field). It needs to be supplied with all API calls that make modifications to a profile.

> 🚧 Organization Accounts
>
> If you have a organization account (ignore this if you do not), you can "impersonate" an admin of a child sub-organization, by supplying `X-Force-Org-Id: org_id_goes_here` HTTP header along with all API calls within the Profiles scope. This will allow you to view, create and modify Profiles within the target sub-organization using the API token of the parent (main) Organization.