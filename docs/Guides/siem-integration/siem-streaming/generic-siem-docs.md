---
title: 'Integration: General Purpose'
excerpt: >-
  Streaming logs to any Fluentbit supported output using our pre-built docker
  container
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

The general and most generic way of receiving logs from Control D's SIEM output integration is by deploying our **pre-built docker container.**

This container securely terminates log data sent from our network to yours, and forwards it on to a SIEM tool within your network.

# Supported Outputs / Log Destinations

Fluentbit [supports many outputs](https://docs.fluentbit.io/manual/pipeline/outputs), all of which change only a small portion of the configuration and generally follow the same structure. As such, this is a generic document that applies to any of the supported outputs, referencing the necessary pages in Fluentbit's docs.

See: [https://docs.fluentbit.io/manual/pipeline/outputs](https://docs.fluentbit.io/manual/pipeline/outputs)

# Pre-Requisites

SIEM log streaming is only available for select organizational customers at this time.

## Customer Side

<Table>
  <thead>
    <tr>
      <th>
        Category
      </th>

      <th>
        Requirements
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Hardware
      </td>

      <td>
        * Virtual Machine<br />- VPS<br />- Baremetal Server (X86 architecture)
      </td>
    </tr>

    <tr>
      <td>
        Operating System
      </td>

      <td>
        Linux Distribution (capable of running Docker Containers / Docker CE)
      </td>
    </tr>

    <tr>
      <td>
        Networking
      </td>

      <td>
        * Public Static IP address (For securely receiving logs from our SIEM integration output over the internet)<br />- TCP/TLS Traffic Capability (If you use a proxy at the edge of your network it must support bare TCP/TLS connections -- this is not HTTP/S!)<br />- Internal network access to your SIEM system (For forwarding logs received into your system)
      </td>
    </tr>

    <tr>
      <td>
        Firewall / Container Port Mappings
      </td>

      <td>
        Permit inbound traffic on `tcp/24224` to the docker container
      </td>
    </tr>

    <tr>
      <td>
        SIEM / Log Streaming Software
      </td>

      <td>
        [FluentBit Supported Outputs](https://docs.fluentbit.io/manual/pipeline/outputs) (Splunk, Elasticsearch, Azure, etc)
      </td>
    </tr>
  </tbody>
</Table>

## Submitting Details to Support

During the Alpha phase you must contact us in order to enroll.

Our system will generate a docker config bundle file for you which you'll use in the successive instructions.

Send an e-mail to [Control D Support](mailto:help@controld.com) asking for the SIEM Integration config bundle with:

* Names or IDs of all Organizations and Sub-Organizations that you require SIEM streaming for
* Public IP address
* *Optional**] D DNS record (if the public IP is prone to changing / dynamic)
* The Analytics Storage Region you plan to use

> 🚧 IMPORTANT: After you have sent us the information required for SIEM streaming, do not change your Analytics Storage Region.

# Installation

1. Install Docker Engine on the host. [Instructions Link](https://docs.docker.com/engine/install/)

2. Upload the config bundle to the host
   ```shell
   scp yourbundle.tar.gz your-linux-host.example.com:/tmp/	
   ```

3. Extract the config + container bundle:
   ```shell
   mkdir logs-receiver
   tar -xvf /tmp/yourbundle.tar.gz -C logs-receiver
   ```

4. Start the container (interactively at first for testing)
   ```shell
   cd logs-receiver
   docker compose up
   ```

5. Confirm that logs are arriving (they won't be going anywhere yet!)

6. Modify the configuration `logs-receiver/fluent-bit.yaml` and update the `outputs:` section to add your desired logs destination.

   >  See [https://docs.fluentbit.io/manual/pipeline/outputs](https://docs.fluentbit.io/manual/pipeline/outputs) for instructions
   >
   > fluent-bit supports a wide variety of log collectors, including ELK, Datadog and Splunk  
   >
   > Example: Splunk

   ```yaml Example: Splunk
   outputs:
     - name: splunk
       host: splunk.example.com                           # Modify 
       splunk_token: 55555555-5555-5555-5555-555555555555 # Modify
       port: 8088                                         # Modify
       tls: on                                            # Modify
       tls.verify: on                                     # Modify
   ```

7. Start the container in `daemon` mode so it continues running when you close your shell: 

   ```bash
   docker compose up --detach
   ```

8. Please notify the Control D support team to confirm that you are receiving logs successfully!

> 🚧 Changing your Analytics Storage Region will break your log streaming - if you wish to do so, please let the Control D support team know and we will issue a new bundle for you

## Troubleshooting

* If your destination system does not receive logs, check the running fluent-bit instance for errors: 
  ```
  docker compose logs --follow
  ```
* If needed, `restart` the `container` with:
  ```bash
  docker compose up --force-recreate --detach
  ```

## Example Config

Here is a sample docker compose file and fluent-bit config that you can use to start a fluentbit receiver on your end. Be mindful this not a working sample. It lists templated components that you will need to comment out or provide. 

More importantly it will not actually receive anything from Control D until we create a custom configuration. Once you're ready to proceed, provide us with the org IDs you wish to receive status for and we'll send you a final config bundles.

```Text docker-compose.yaml
version: "3.7"

services:
  fluent-bit:
    image: fluent/fluent-bit
    command: ["/fluent-bit/bin/fluent-bit", "-c", "/fluent-bit/etc/fluent-bit.yaml"]
    volumes:
      - ./fluent-bit.yaml:/fluent-bit/etc/fluent-bit.yaml
      - ./certs:/etc/ssl/fluent-bit-certs
    ports:
      - "24224:24224"

```
```Text fluent-bit.yaml
---
pipeline:
  inputs:
    - name: forward
      tls: on
      tls.verify: "on"
      tls.ca_file: /etc/ssl/fluent-bit-certs/${CN}-ca.pem
      tls.crt_file: /etc/ssl/fluent-bit-certs/${CN}-cert.pem
      tls.key_file: /etc/ssl/fluent-bit-certs/${CN}-privkey.pem
  outputs:
    # Edit this!
    # See https://docs.fluentbit.io/manual/pipeline/outputs for a full list of supported outputs

    # Output logs in JSON format to the container's standard output
    # Can be used to validate logs are being received, but typically should be disabled in production
    - name: stdout
      match: '*'
      format: json

    # Splunk Example
    # https://docs.fluentbit.io/manual/pipeline/outputs/splunk
    # - name: splunk
    #   host: splunk.example.com # change me
    #   splunk_token: 55555555-5555-5555-5555-555555555555 # change me
    #   match: '*'
    #   port: 8088
    #   tls: on
    #   tls.verify: on

```
