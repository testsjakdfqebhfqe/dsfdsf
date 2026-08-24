---
title: MikroTik RouterOS
excerpt: Using Control D on MikroTik Devices.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Using Control D on MikroTik RouterOS with native DoH:

MikroTik's RouterOS has native support for DoH.

<Callout icon="📘" theme="info">
  As of RouterOS Version 7.19 - MikroTik has included a built-in root certificate authorities store.
</Callout>

You can enable the built-in Certificate Store by running the following:

```shell
/certificate/settings/set builtin-trust-anchors=trusted
```

It's recommended to add Control D's DNS IP to your router for redundancy by running:

```shell
/ip dns set servers=76.76.2.22
```

### Enabling DoH:

Run the following to enable your Control D DoH Resolver:

```shell shell
/ip dns set use-doh-server=https://dns.controld.com/$RESOLVER-ID allow-remote-requests=yes verify-doh-cert=yes
```

### Verifying DoH:

Run `ip dns print without-paging` to verify your settings:

```
[admin@MikroTik] > ip dns print without-paging
                      servers: 76.76.2.22
              dynamic-servers:
               use-doh-server: https://dns.controld.com/$RESOLVER-ID
              verify-doh-cert: yes
   doh-max-server-connections: 5
   doh-max-concurrent-queries: 50
                  doh-timeout: 5s
        allow-remote-requests: yes
          max-udp-packet-size: 4096
         query-server-timeout: 2s
          query-total-timeout: 10s
       max-concurrent-queries: 100
  max-concurrent-tcp-sessions: 20
                   cache-size: 2048KiB
                cache-max-ttl: 1w
      address-list-extra-time: 0s
                          vrf: main
           mdns-repeat-ifaces:
                   cache-used: 36KiB
```

### Testing your DoH Settings:

Let's verify that your RouterOS Device is using Control D.

* From the CLI run: `tool/sniffer/quick port=443 ip-address=76.76.2.22`
* Open another Terminal and connect to your MikroTik Router _without exiting the previous terminal_.
* Run the following: ` resolve domain-name=verify.controld.com`
* If successful, the previous command should return no output.
* You can verify the query against your RouterOS Endpoint Activity Logs in the Web Dashboard.

***

> 📘 Limiting background activity to save resources:

When using the `verify-doh-cert=yes` on lower spec devices (like [hEX S](https://mikrotik.com/product/hex_s)) you will likely encounter instability and crashing. This is due to RouterOS's DoH implementation checking the `CRL` _for each certificate in the chain_ causing Out-Of-Memory errors and crashes. This can be `/certificate/settings/set crl-use=no` to conserve system resources, however this greatly reduces your DNS Security.