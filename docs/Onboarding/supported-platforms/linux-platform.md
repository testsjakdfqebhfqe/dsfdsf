---
title: Linux
excerpt: How to configure Control D on any Linux computer.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Automatic Setup (CLI)

Want to spend the least amount of time setting up Control D on a Linux device or looking to do a scripted deployment? Have no fear, there is an app for that. 

[Command Line Daemon](doc:ctrld) is what you're looking for.

# Manual Setup

Want to update the DNS server in your favorite Linux distro? Well, there are *only* about 20 ways to do it. But in all seriousness, if you require a tutorial to do this, it may be a better idea to use the Automatic Setup method. It abstracts the setup to a single command. 

We'll briefly go over some common ways to update DNS. 

## systemd-resolve

If you are running a version of Linux that uses systemd-resolved, you can likely configure DNS-Over-TLS on it.

Open Terminal and edit your resolved.conf file

```
nano /etc/systemd/resolved.conf
```

### Premium Resolvers

Update your config as follows if you are using a custom premium resolver. `abcd1234` will be different for you. 

```
[Resolve]

DNS=76.76.2.22#abcd1234.dns.controld.com

DNSOverTLS=yes
```

The value of `DNS` after the `#` will be your DNS-over-TLS resolver for the chosen Endpoint. 

Save the file and restart the systemd-resolve service. 

### Free Resolvers

Update your config templating `DNS` after the `#` to the DNS-over-TLS hostname for the desired free resolver. 

```
[Resolve]

DNS=76.76.2.11#p2.freedns.controld.com

DNSOverTLS=yes
```

The above example assumes the Malware and Ads blocking resolver.

Save the file and restart the systemd-resolve service.

## stubby

If you're using stubby, edit the config file.

```
sudo nano /etc/stubby/stubby.yml
```

Find `round_robin_upstreams` and set this value to `0`. 

Then search for **DEFAULT UPSTREAMS** and and comment out all of them. Then add a new config block. 

### Premium Resolvers

Add the following entry to your config file. 

```
- address_data: 76.76.2.22
  tls_auth_name: "abcd1234.dns.controld.com"
```

The value of `tls_auth_name` will be your DNS-over-TLS resolver for the chosen Endpoint (`abcd1234` will be different for you). If you need additional backup IPs or IPv6, refer to [Control D IP Ranges](doc:control-d-ip-ranges). 

Save this file and restart stubby.

### Free Resolvers

Add the following entry to your config file.

```
- address_data: 76.76.2.11
  tls_auth_name: "p2.free.controld.com"
```

The value of `tls_auth_name` will be the desired free resolver DNS-over-TLS hostname. The above example assumes the Malware and Ads blocking resolver. If you need additional backup IPs or IPv6, refer to [Control D IP Ranges](doc:control-d-ip-ranges).

Save this file and restart stubby.
