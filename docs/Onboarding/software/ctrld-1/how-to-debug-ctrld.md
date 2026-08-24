---
title: How to Debug ctrld
excerpt: >-
  Anything made by humans is not perfect, let's get some data and resolve the
  issue, shall we?
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Basic Debug Logging

ctld keeps a always-on debug log while the process is running. In order to send the debug log, open admin Command Line or Terminal on a machine running ctrld, and run this command: `ctrld log send`. 

Then reach out to us, and provide the **Endpoint name** that was configured on this machine, and we can analyze the logs. Normally, the Endpoint name will be the machine hostname. 

# Full Debug Logging

In order to enable full debug logging with `ctrld`, here is what you have to do. 

## Windows

### Enable Full Logging

1. Open admin `cmd` or Powershell and navigate to `C:/ControlD`
2. Run this exact command: `ctrld start --log dns.log`

ctrld will start/restart in full debug mode, and write debug data to `C:/ControlD/dns.log`.

Reproduce the issue, copy the file and send it to us. 

### Disable Full Logging

Once you've collected the logs, it's a good idea to stop writing the debug log file, which can become quite large over time. To do this you can either re-run the installer as you did originally, or:

1. Open admin `cmd` or Powershell and navigate to `C:/ControlD`
2. Run this command: `ctrld start --cd RESOLVER_ID_GOES_HERE`

Template the value of `RESOLVER_ID_GOES_HERE` with your Endpoint's actual Resolver ID. 

![](https://files.readme.io/d0971c2ab5ccff752e3182fa290fd066505714aa527af499c2ee72bf5358e008-image.png)

## MacOS

### Enable Full Logging

1. Open Terminal  and run run this exact command: `sudo ctrld start --log ~/dns.log`

ctrld will start/restart in full debug mode, and write debug data to the user's home directory. 

Reproduce the issue, copy the file and send it to us.

### Disable Full Logging

Once you've collected the logs, it's a good idea to stop writing the debug log file, which can become quite large over time. To do this you can either re-run the installer as you did originally, or:

1. Open Terminal and run this command: `ctrld start --cd RESOLVER_ID_GOES_HERE`

Template the value of `RESOLVER_ID_GOES_HERE` with your Endpoint's actual Resolver ID.
