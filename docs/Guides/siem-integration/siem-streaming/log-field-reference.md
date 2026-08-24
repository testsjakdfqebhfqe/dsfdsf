---
title: Log Field Reference
excerpt: >-
  All of the fields available in the log data supplied by the SIEM log streaming
  integration.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `time`
      </td>

      <td>
        String containing RFC3339 Datetime
      </td>

      <td>
        The time the query occurred
      </td>
    </tr>

    <tr>
      <td>
        `query`
      </td>

      <td>
        string
      </td>

      <td>
        The domain queried, also called `question`
      </td>
    </tr>

    <tr>
      <td>
        `query_type`
      </td>

      <td>
        string
      </td>

      <td>
        The RR Type
      </td>
    </tr>

    <tr>
      <td>
        `src_ip`
      </td>

      <td>
        string
      </td>

      <td>
        The IP from which the request came
      </td>
    </tr>

    <tr>
      <td>
        `reply_code_id`
      </td>

      <td>
        integer
      </td>

      <td>
        The DNS status code
      </td>
    </tr>

    <tr>
      <td>
        `protocol`
      </td>

      <td>
        string (enum)
      </td>

      <td>
        The DNS protocol used:  

        * `legacy`
        * `doh`
        * `doh3`
        * `dot`
        * `doq`
      </td>
    </tr>

    <tr>
      <td>
        `answers`
      </td>

      <td>
        object
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        `answers.ips`
      </td>

      <td>
        array`<string>`
      </td>

      <td>
        List of all answers provided. Currently only contains IPs.
      </td>
    </tr>

    <tr>
      <td>
        `answers.geoip`
      </td>

      <td>
        object (optional)
      </td>

      <td>
        GeoIP2 information about the first valid IP in the answers.
      </td>
    </tr>

    <tr>
      <td>
        `answers.geoip.countryCode`
      </td>

      <td>
        string (optional)
      </td>

      <td>
        two-letter country code of the IP
      </td>
    </tr>

    <tr>
      <td>
        `answers.geoip.city`
      </td>

      <td>
        string (optional)
      </td>

      <td>
        Name of the city of the IP
      </td>
    </tr>

    <tr>
      <td>
        `answers.geoip.isp`
      </td>

      <td>
        string (optional)
      </td>

      <td>
        Name of the ISP of the IP
      </td>
    </tr>

    <tr>
      <td>
        `answers.geoip.asn`
      </td>

      <td>
        integer (optional)
      </td>

      <td>
        ASN number of the ISP
      </td>
    </tr>

    <tr>
      <td>
        `organisation`
      </td>

      <td>
        object
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        `organisation.id`
      </td>

      <td>
        string
      </td>

      <td>
        the ID of the organisation account
      </td>
    </tr>

    <tr>
      <td>
        `organisation.name`
      </td>

      <td>
        name
      </td>

      <td>
        the name of the organisation (currently not supplied)
      </td>
    </tr>

    <tr>
      <td>
        `user`
      </td>

      <td>
        object (null  if organisation is not null)
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        `user.id`
      </td>

      <td>
        string
      </td>

      <td>
        the ID of the user account
      </td>
    </tr>

    <tr>
      <td>
        `user.name`
      </td>

      <td>
        string
      </td>

      <td>
        the name of the user (currently not supplied)
      </td>
    </tr>

    <tr>
      <td>
        `device`
      </td>

      <td>
        object
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        `device.id`
      </td>

      <td>
        string
      </td>

      <td>
        the ID of the endpoint
      </td>
    </tr>

    <tr>
      <td>
        `device.name`
      </td>

      <td>
        string
      </td>

      <td>
        the name of the endpoint
      </td>
    </tr>

    <tr>
      <td>
        `client`
      </td>

      <td>
        object (optional)
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        `client.id`
      </td>

      <td>
        string
      </td>

      <td>
        the ID of the client
      </td>
    </tr>

    <tr>
      <td>
        `client.name`
      </td>

      <td>
        string
      </td>

      <td>
        the name of the client (usually hostname or custom alias)
      </td>
    </tr>

    <tr>
      <td>
        `controld_action`
      </td>

      <td>
        integer
      </td>

      <td>
        The action taken by Control D  

        * `-1` Request Failed
        * `0` Blocked
        * `1` Bypassed
        * `2` Redirected (IP)
        * `3` Redirected (Location)
      </td>
    </tr>

    <tr>
      <td>
        `controld_trigger`
      </td>

      <td>
        string (optional)
      </td>

      <td>
        The reason the action was taken  

        * `default` default action
        * `filter` blocked by filter
        * `service` action triggered by service
        * `custom` custom rule
        * `grule` global rule
        * `rebind` rebind protection
      </td>
    </tr>

    <tr>
      <td>
        `controld_trigger_name`
      </td>

      <td>
        string (optional)
      </td>

      <td>
        The label for the trigger described above, if any.  

        * `filter`: the name of the filter
        * `forservice`: the name of the service
        * `forcustom`: the name of the custom rule
      </td>
    </tr>

    <tr>
      <td>
        `controld_spoof_target`
      </td>

      <td>
        string (optional)
      </td>

      <td>
        The target of a redirect, if any. Generally an IP, another domain, or an IATA code of a proxy location.
      </td>
    </tr>

    <tr>
      <td>
        `domain_category`
      </td>

      <td>
        string (optional)
      </td>

      <td>
        A broad category of the type of website, such as `business` or `entertainment`. Not currently supplied
      </td>
    </tr>

    <tr>
      <td>
        `source_ip`
      </td>

      <td>
        object (optional)
      </td>

      <td>
        Contains the same info as answers.geoip (see above), but for `src_ip`
      </td>
    </tr>
  </tbody>
</Table>