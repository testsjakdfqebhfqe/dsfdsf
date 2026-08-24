---
title: SIEM Log Streaming with Fluent Bit (Alpha)
excerpt: Stream logs from Control D into your SIEM solution.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Control D supports SIEM Log streaming using Fluent Bit (in Alpha) for select organization customers.

We chose Fluent Bit for exporting log data to SIEM (Security Information and Event Management) solutions because of its:

* **Flexible Output Formats**: Send logs to [various Fluent Bit supported outputs](https://docs.fluentbit.io/manual/pipeline/outputs) like Splunk, S3, or Elasticsearch (all major platforms supported)
* **Secure Transmission**: The system uses well known TLS encryption to ensure secure log transmission between components⁠ (forwarders and receivers)⁠​
* **Isolated Customer Data**: Each customer gets their own Fluent Bit forwarder which prevents configuration errors from affecting other customers and ensures better security isolation⁠.

# Links

Check out the Integration documentation and Log Field reference below:

* [Integration: General Purpose](generic-siem-docs)
* [Integration: Splunk](https://docs.controld.com/docs/splunk-integration)
* [Log Field Reference](https://docs.controld.com/docs/log-field-reference)

# Architecture

<Image align="center" border={true} src="https://files.readme.io/33d539fbda398c81f237a4d59ef50bd9d9fddd0629f578f2533aafaf42a0087f-image.png" className="border" />

<br />

## Outbound IP addresses (allowlisting)

If your SIEM receiver (or upstream firewall/WAF) only accepts traffic from known sources, you can allowlist the outbound (egress) IP addresses used by Control D’s SIEM log streaming senders.

**Current sender egress IPs:**

| Region | Hostname                    | IP               |
| ------ | --------------------------- | ---------------- |
| JFK    | `jfk-siem-sender-poc-org01` | `34.48.76.218`   |
| SYD    | `syd-siem-sender-poc-org01` | `34.116.103.149` |
| AMS    | `ams-siem-sender-poc-org01` | `34.141.202.141` |

**Notes**

* These IPs are intended for **source allowlisting** only (the IPs your SIEM will see as the sender).
* **Subject to change:** while these are static today, infrastructure changes may require updates. Contact support if your environment can’t tolerate changes.
