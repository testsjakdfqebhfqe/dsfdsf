---
api:
  file: control-d.json
  operationId: put_profiles-profile-id-services-service
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
## do

* `0` - Block service domains 
* `1` - Bypass service domains (to override Filter block)
* `2` - Spoof service domains to IP
* `3` - redirect service domains via proxy

## status

* `0` - rule is disabled
* `1` - rule is enabled

## via

* In `do=2` mode, this arg  supplies the `A` record or `CNAME`. 
* In `do=3` mode, this arg supplies a 3 letter IATA code proxy identifier. View all options via [List Proxies](ref:get_proxies) .

## via\_v6

* In `do=2` mode, this arg  supplies the `AAAA` record
* No effect when `do=3`