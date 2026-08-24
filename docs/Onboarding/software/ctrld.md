---
title: Command Line Daemon
excerpt: DNS proxy server you can run on a router, or any other device.
hidden: true
metadata:
  robots: index
---
In order to facilitate simple onboarding, on any type of device (with a keyboard) we've developed an open source  command line daemon, known as **ctrld**. It can be used to configure a Control D [Device](doc:devices) with a single command, and it can do a whole bunch more. 

# Why Use This

You may want to use this utility in the following situations:

* You operate a network, and have to use Legacy DNS for all your LAN clients 
* Want to use Secure DNS protocols on a device that does not support them
* Want to create an advanced DNS routing policies or leverage split horizon DNS 
* Want to see all your [LAN clients](doc:device-clients), and create DNS policies for all of them via a web GUI
* Want to deploy Secure DNS on a roaming client 


> 📘 Need custom TOML while staying dashboard-managed?
>
> If you installed `ctrld` with the Control D one-line installer or started it with `--cd`, the local `ctrld.toml` file is generated from the Control D API and is not the durable source of truth. Use the dashboard TOML Config editor for persistent managed custom TOML.
>
> See [Managed Custom ctrld TOML Config](doc:managed-custom-ctrld-toml-config) for the dashboard-managed path, or [ctrld Local Config Mode vs CD Mode](doc:ctrld-local-config-vs-cd-mode) if you want to understand when local files are authoritative.

# Quick Install

The simplest way to start using `ctrld` is to run the installer. Open an terminal and execute this command as admin/system user on any Linux or UNIX-like OS (including MacOS):

```text bash
sh -c 'sh -c "$(curl -sL https://api.controld.com/dl)" -s RESOLVER_ID_HERE forced'
```

 Template `RESOLVER_ID_HERE` with your actual Resolver ID from the relevant Device. 

If you'd like to use the same method on Windows, run this in Powershell:

```Text cmd
(Invoke-WebRequest -Uri 'https://api.controld.com/dl/ps1' -UseBasicParsing).Content | Set-Content "$env:TEMPctrld_install.ps1"; Invoke-Expression "& '$env:TEMPctrld_install.ps1' 'RESOLVER_ID_HERE' 'forced'"
```

The above scripts will do the following:

* Detect your OS and architecture 
* Download the appropriate binary 
* Make it executable
* Register a system service and start the DNS server
* Modify the DNS settings on your network adapter to use the local server

In order to skip the interactive confirmation (y/n), simply append `forced` flag to the installer command. ie. `-s RESOLVER_ID_HERE forced` for MacOS and Linux, and `RESOLVER_ID_HERE forced` for Windows + PowerShell. This will perform the installation without any user confirmation or input.  

# Download Manually

[Head over to Github](https://github.com/Control-D-Inc/ctrld), and download the version of the daemon for your platform. You can find builds for most operating systems in the [Releases](https://github.com/Control-D-Inc/ctrld/releases) section. 

Currently supported operating systems are:

* Windows (386, AMD64 and ARM) - use the `_windows` builds
* Mac (AMD64 and ARM) - use the `_darwin` builds 
* Linux (386, AMD64, ARM, MIPS) - use the `_linux` builds
* FreeBSD (386, AMD64, ARM) - use the `_freebsd` builds 

![](https://files.readme.io/4bb9d1b-image.png)

# Get your resolver ID

When you create a Control D Device, you are issued a set of DNS resolvers. On the screen that shows you your resolvers, you will see "Resolver ID" at the top. 

# Windows

## Start Service

Open Administrative command line, and navigate to the folder where the .exe file is extracted, and run this command. 

```
ctrld.exe start --cd RESOLVER_ID_HERE
```

This command will do the following:

* Fetch your Device's configuration
* Render a configuration file and store it in the HOME directory
* Spawn a DNS listener and start a system service that will always run
* Configure the DNS on the default interface to use the local DNS proxy server

## Stop Service

In order to **temporarily stop** the Control D service, execute the following from Administrative command line:

```
ctrld.exe stop
```

> 🚧 Service is still installed
>
> The above commands will stop the service, and unconfigure the listener it spawned from the default interface. If the system is rebooted, the original configuration will be restored automatically.

## Uninstall Service

In order to permanently uninstall `ctrld` run this command. 

```
ctrld.exe uninstall
```

`ctrld` binary will remain on disk and can be used at a later time. To remove all files from disk, append `--cleanup` flag to the uninstall command. 

# MacOS

## Start Service

Open terminal, navigate to the folder where the binary file is extracted, and run this command. 

```
sudo ctrld start --cd RESOLVER_ID_HERE
```

This command will do the following:

* Fetch your Device's configuration
* Render a configuration file and store it in the HOME directory
* Spawn a DNS listener and start a system service that will always run
* Configure the DNS on the default interface to use the local DNS proxy server

## Stop Service

In order to **temporarily stop** the Control D service, execute the following command with admin/sudo privilege:

```
sudo ctrld stop
```

> 🚧 Service is still installed
>
> The above commands will stop the service, and unconfigure the listener it spawned from the default interface. If the system is rebooted, the original configuration will be restored automatically.

## Uninstall Service

In order to permanently uninstall `ctrld` run this commands

```
sudo ctrld uninstall
```

`ctrld` binary will remain on disk and can be used at a later time. To remove all files from disk, append `--cleanup` flag to the uninstall command.

# Linux

## Start Service

Open terminal, navigate to the folder where the binary file is extracted, and run this command. 

```
sudo ctrld start --cd RESOLVER_ID_HERE
```

This command will do the following:

* Fetch your Device's configuration
* Render a configuration file and store it in the HOME directory
* Spawn a DNS listener and start a system service that will always run
* Configure the DNS on the default interface to use the local DNS proxy server

## Stop Service

In order to **temporarily stop** the Control D service, execute the following command with admin/sudo privilege:

```
sudo ctrld stop
```

> 🚧 Service is still installed
>
> The above commands will stop the service, and unconfigure the listener it spawned from the default interface. If the system is rebooted, the original configuration will be restored automatically.

## Uninstall Service

In order to permanently uninstall `ctrld` run this command.

```
sudo ctrld uninstall
```

If you are running `ctrld` on a router, you may need to run the above command from the directory where you installed it. `sudo` may be optional if you're running it as a root user. 

`ctrld` binary will remain on disk and can be used at a later time. To remove all files from disk, append `--cleanup` flag to the uninstall command.

# Routers

`ctrld` currently supports the following routers and firmware:

* ASUS Merlin
* DD-WRT
* Firewalla
* Fresh Tomato
* GL.iNet
* OpenWRT
* pfSense / OPNsense
* Synology
* Ubiquiti UDM, UDR, EdgeOS

All you have to do is SSH into your router and follow the **Quick Install** instructions at the top of this page. With a single command, you can start using Control D in literally seconds. 

# Remote Uninstallation

Simply delete the associated Device from the web control panel. The DNS daemon will self-uninstall if you're using v1.3.9 or newer. 

# Upgrade

In order to upgrade the `ctrld` service to the latest version, there are two ways to do it. 

1. Simply re-run the installer command without any args. Use this method if you're running v1.3.7 or earlier. 
2. Run `ctrld upgrade` command. This is the recommended method. 

## Windows

Run this batch command in admin cmd (not Powershell). Use this if you're running v1.3.7 or earlier. 

```
powershell -Command "(Invoke-WebRequest -Uri 'https://api.controld.com/dl' -UseBasicParsing).Content | Set-Content '%TEMP%\ctrld_install.bat'" && %TEMP%\ctrld_install.bat
```

or

```
ctrld upgrade
```

## Linux or Mac

Run this bash command in Terminal as root user.  

```Text bash
sh -c 'sh -c "$(curl -sL https://api.controld.com/dl)"'
```

or

```
ctrld upgrade
```

## Update Channels

There are 2 update channels:

* `prod` - stable production release (default)
* `dev` - beta release that is ahead of production 

To switch channels, append the channel name to the upgrade command:

```
C:\Windows\system32>ctrld upgrade prod
Jul 22 13:21:56.000 NTC Upgrade successful - v1.3.7


C:\Windows\system32>ctrld upgrade dev
Jul 22 13:22:54.000 NTC Upgrade successful - dev-429123b
```

# Do More

This is the most basic use of the `ctrld` daemon. It can do a whole lot more, especially if you run it on a router. What can you do with it? Here are some use cases:

1. Create unique DNS routing policies based on source IP, device hostname or MAC address
2. Split horizon DNS with wildcard rules
3. Use Secure DNS protocols even for devices that don't support them (UDP53-to-DOH)
4. Run multiple DNS listeners, with unique policies and variable upstreams
5. Cache DNS records locally 

For a full feature set, please [check out the README](https://github.com/Control-D-Inc/ctrld#readme).

## Example Configs

Want to craft your own config? For dashboard-managed custom TOML, start with [Managed Custom ctrld TOML Config](doc:managed-custom-ctrld-toml-config). If you want a local file to be authoritative, see [ctrld Local Config Mode vs CD Mode](doc:ctrld-local-config-vs-cd-mode). You can also check out additional [example configurations](https://github.com/Control-D-Inc/ctrld/wiki/Example-Configurations).

## Troubleshooting

Something not working? Start with [How to Debug ctrld](doc:how-to-debug-ctrld) to collect logs, then check [ctrld Known Issues](doc:ctrld-known-issues) for current platform-specific caveats and workarounds.