---
title: Root Certificate Installation
excerpt: How to install a custom root certificate in order to have skinned block pages.
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

Installation of the Control D root certificate is a requirement in order to see a customized block page in a browser when attempting to access blocked HTTPS resources as dictated by the configuration within the profile applied to a device or user.

Without the root certificate a user will receive a TLS error in their browser when trying to visit a blocked webpage that uses HTTPS.  With the root certificate installed the user will be presented with a webpage explaining that their request has been blocked by Control D per their configured rules.

# Installation instructions

Use the following instructions to install on your operating system or browser.

## Operating Systems

### Microsoft Windows

#### GUI

1. Download the Control D cer file: [Control-D-root-x1.cer](https://deploy.controld.com/blockpage/Control-D-root-x1.cer) 
2. Double click to open `Control D Blockpage CA X1.crt` file (the *Certificate* window will open)
3. Click on **Install Certificate**.
4. In the **Certificate Import Wizard**, when prompted for the Certificate Store, choose *Place all certificates in the following store* and select the **Trusted Root Certification Authorities** store.

#### PowerShell

Run the following PowerShell script as an administrator. 

> 📘 You can also add this as a script in your favourite RMM to mass deploy the certificate to Windows machines.

```powershell
# Define the URL and local file path
$url = "https://deploy.controld.com/blockpage/Control-D-root-x1.cer"
$localPath = "C:\Temp\Control-D-root-x1.cer"

# Create directory if it doesn't exist
if (!(Test-Path "C:\Temp")) {
    New-Item -Path "C:\Temp" -ItemType Directory
}

# Download the certificate
Invoke-WebRequest -Uri $url -OutFile $localPath

# Import the certificate to the Trusted Root Certification Authorities store
$cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$cert.Import($localPath)

$store = New-Object System.Security.Cryptography.X509Certificates.X509Store "Root", "LocalMachine"
$store.Open("ReadWrite")
$store.Add($cert)
$store.Close()

# Clean up the downloaded certificate file
Remove-Item $localPath
```

### Linux

#### Debian-based distros

The following steps are assuming you are logged into a root account and that you have the `ca-certificates` and `wget` packages installed.

```shell
wget https://deploy.controld.com/blockpage/Control-D-root-x1.cer -O /usr/local/share/ca-certificates/Control-D-root-x1.cer
update-ca-certificates
```

#### Fedora-based distros

The following steps are assuming you are logged into a root account and that you have the `p11-kit-trust` and `wget` packages installed.

```shell
wget https://deploy.controld.com/blockpage/Control-D-root-x1.cer -O /tmp/Control-D-root-x1.cer
trust anchor /tmp/Control-D-root-x1.cer
```

### Apple MacOS

#### GUI

1. Download the Control D cer file:  [Control-D-root-x1.cer](https://deploy.controld.com/blockpage/Control-D-root-x1.cer) 
2. Double click to open `Control D Blockpage CA X1.crt` file  (the *Keychain Access.app* will open with the list of Certificates installed on your computer).
3. Double-click on `Control D Blockpage CA X1` in that list.
4. Under **Trust**, choose **Always Trust** for **Secure Socket Layers (SSL)**.
5. Close the window.  Mac OS may prompt you to enter your administrative password

#### Shell

Run the following script.

> 📘 You can also add this as a script in your favourite RMM to mass deploy the certificate to MacOS machines

```shell
#!/bin/bash

# Define URL and local path
URL="https://deploy.controld.com/blockpage/Control-D-root-x1.cer"
LOCAL_PATH="/tmp/Control-D-root-x1.cer"

# Download the certificate
curl -o $LOCAL_PATH $URL

# Install the certificate
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain $LOCAL_PATH

# Clean up
rm $LOCAL_PATH
```

### iOS / iPadOS

1. Launch Safari and open  [Control-D-root-x1.cer](https://deploy.controld.com/blockpage/Control-D-root-x1.cer) , then choose **Allow**.
2. Open the Settings app, then go to General → Profiles.
3. Open `Control D Blockpage CA X1` then **Install**.
4. In the Settings app, go to General → About → Certificate Trust Settings.
5. Enable Full Trust for `Control D Blockpage CA X1`

### Android

1. Launch your browser and navigate to  [Control-D-root-x1.cer](https://deploy.controld.com/blockpage/Control-D-root-x1.cer) 
2. Open the downloaded `Control D Blockpage CA X1.crt` file.
3. When asked, name the certificate **Control D**.

## Web Browsers

### Firefox

Firefox uses it’s on internal certificate store, rather then relying on the system trust, therefore you need to install the cert directly in Firefox.

1. Download the cer file by browsing to  [Control-D-root-x1.cer](https://deploy.controld.com/blockpage/Control-D-root-x1.cer) 
2. In Firefox, open `about:preferences` → Privacy & Security.
3. Scroll down to **Certificates** and click **View Certificates**
4. In the **Authorities** tab click **Import.**
5. Select the **Control-D-root-x1.cer** file.
6. Check **Trust this CA to identify websites** then click **OK**

### Chrome

On Windows and Mac OS Chrome uses the system trust store by default, so adding the certificate to your OS trust as described above is sufficient.

For Linux only, you may need to add our root cert manually on Chrome-based browsers:

1. Open  [Control-D-root-x1.cer](https://deploy.controld.com/blockpage/Control-D-root-x1.cer) to download the **Control-D-root-x1.cer** file.
2. Open `chrome://settings/certificates`
3. In the **Authorities** tab click **Import.**
4. In the lower right, select **All Files**
5. Select the **Control-D-root-x1.cer** file.
6. Check **Trust this certificate for identifying websites** then click **OK**.

### Safari

Safari uses the system certificate store on Mac OS, therefore following the Mac OS instructions above will allow Safari to trust our certificate.

### Brave

Like with other Chromium-based browsers, Brave will use the system certificate store by default. 

# Security Implications for your Organization

The installation of any third party root certificate into a root certificate store should only be done after careful consideration. 

💡 A third party root certificate is any root certificate entrusted by the operating system or browser that it does not ship or come with out of the box.

The implication in doing so is that you are potentially entrusting the certificate authority of that certificate with ALL data which is encrypted inside of ANY TLS connection made at either the OS or browser level.

**To be specific — An operator of a root certificate authority which is entrusted by an end user (browser or operating system) has the technical ability to impersonate any TLS-protected resource on the internet.**

As an example, said operator could put together a fake login page for a bank, and anyone with their root certificate installed would be able to visit the fake website without any browser warning (which would  otherwise appear if someone was trying to do this without the root certificate installed). 

This carries some very serious consequences. As such, before installing a third party root certificate you should carefully consider if it’s required for your organization to see custom block pages.

# Why is this even required in the first place?

When using Control D the user has the ability to block or allow DNS records (and in turn, websites). 

When a DNS record is configured to be blocked we respond with a non-existent IP address (`0.0.0.0`) which results in a timeout error in your browser.

If we were to point blocked DNS records to an IP address where we are serving a block page but **without** the end user having installed our third party root certificate the user would see a TLS error in their browser which is suggestive that there is a man in the middle attack taking place (this is a good thing under most circumstances — you want your browser to tell you this!)

However In order to display a clear and concise block message (and not an error from the browser) when a DNS record is blocked while the user is trying to reach an HTTPS website the user **must install a third party root certificate.**

> 📘 Roll Your Own
>
> You can also create your own root certificate, and [perform your own](https://dev.to/suntong/a-short-guide-on-squid-transparent-proxy-ssl-bumping-k5c) TLS interception. That way, you're entirely in control.

## Example Request Flow

### Normal Conditions (Without Control D Blocking, Pre-installed Root Certificates Only)

Let’s examine what happens when you try to visit [https://google.com](https://google.com) in a web browser under normal conditions.

1. Your web browser queries the OS-configured or browser-configured DNS resolver for `google.com`
2. The configured DNS resolver responds with the IP address for the DNS record

   ```text bash
   ;; ANSWER SECTION:
   google.com.		208	IN	A	142.250.217.110
   ```
3. Your web browser connects to the IP supplied in the DNS response (Google’s real servers)
   1. In the initial TLS handshake (called `ClientHello`) the DNS record `[google.com](http://google.com)` is supplied
   2. The server acknowledges that it is accepting traffic for this DNS record (`ServerHello`) and returns the server-side TLS certificate which is valid for `google.com` (the requested resource)
   3. With the server certificate in hand, the browser checks its trusted root certificate store to see if there is a validate certificate authority which matches with the issuer of the server certificate returned. 
      1. If there is a valid certificate authority (Issuer) in the root store, the browser entrusts this TLS connection and proceeds to pass data.
      2. If there is no valid certificate authority (issuer) in the root store, the browser will show an error message.
4. With the browser trusting the server certificate per the last step, it will proceed to leverage the established TLS connection to pass encrypted HTTP requests inside of it **and then download and render the unmodified and original google.com webpage appropriately.** 

### Block Condition (Control D Configured to Block a DNS Record)

1. Your web browser queries the OS-configured or browser-configured DNS resolver for `google.com`
2. The configured DNS resolver responds with the IP address for the DNS record

   ```text
   ;; ANSWER SECTION:
   google.com.		208	IN	A	1.2.3.4
   ```

   ⚠️ Note that the IP `1.2.3.4` represents a placeholder for an IP address which Control D operates and **NOT** the true IP address!

   Your web browser connects to the IP supplied in the DNS response (**in this case a Control D operated block-page server**)
3. 1. In the initial TLS handshake (called `ClientHello`) the DNS record `[google.com](http://google.com)` is supplied
   2. The server acknowledges that it is accepting traffic for this DNS record (`ServerHello`) and returns the server-side TLS certificate which is valid for `google.com` (the requested resource) with the difference that the server certificate is signed and issued by the `Control D Blockpage` Certificate Authority rather than `Google, Inc` .
   3. With the server certificate in hand, the browser checks its trusted root certificate store to see if there is a validate certificate authority which matches with the issuer of the server certificate returned. 
      1. If there is a valid certificate authority (Issuer) in the root store, the browser entrusts this TLS connection and proceeds to pass data. 
      2. If there is no valid certificate authority (issuer) in the root store, the browser will show an error message.
4. With the browser trusting the server certificate per the last step, it will proceed to leverage the established TLS connection to pass encrypted HTTP requests inside of it **and then download and render the block page which is returned from Control D operated servers.** 

# Minimizing Operational Risk with our Root Certificate Authority

Because we are asking for a high level of trust from our customers when installing our root certificate it is important to explain how our root certificate is used and the precautions we take to avoid misuse.

* We employ industry standard best practices for operating our PKI (Public Key Infrastructure)
  * Chained certificate authorities (Separate root and intermediate authorities)
  * Offline root certificate storage
    * The private key for our root certificate (the one you install) was generated offline and is stored on a thumb drive in a secure location offline (so called “cold storage”).
    * It cannot be accessed without physically being in possession of the drive, and is not possible to obtain over the internet.
* The server certificates used on our block page server are generated with short lifetimes of `72h` and only on demand/as needed.
  * When a request arrives for a blocked website on our block page server, if a server certificate matching a blocked domain does not already exist or has expired the block page server requests issuance of this certificate from the intermediate certificate authority in-line with your request.
  * It is only possible for the block page server to issue short lived certificates signed by the intermediate authority.
* We secure all of our servers using industry standard best practices and monitor for intrusions wherever possible
* We maintain our software and patch on a recurring basis, and immediately whenever a security vulnerability is discovered
