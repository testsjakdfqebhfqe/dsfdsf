---
title: JAMF NOW Deployment (iOS / tvOS)
deprecated: false
hidden: true
metadata:
  robots: index
---
# 📘 **JAMF NOW Deployment (iOS / tvOS)**

<br />

## **Overview**

This guide explains how to enforce Control D DNS on **iOS** and **tvOS** devices using **Jamf Now** by uploading a custom `.mobileconfig` that includes Apple’s `DNS Settings` payload. This works even when devices are:

* Not DEP-enrolled
* Not supervised
* BYOD
* Manually enrolled via a web link

Control D DNS will apply system-wide as long as the MDM profile remains installed.

***

## **Requirements**

❯ A **Jamf Now** account
❯ An iPhone/iPad/tvOS device enrolled in Jamf Now
❯ A **Control D Resolver ID**
❯ Ability to upload a custom configuration profile

***

## **Step 1 — Get Your Control D Endpoint**

In the Control D Dashboard:

1. Go to **Devices**
2. Create/select a Device
3. Copy your DoH endpoint:

```
https://dns.controld.com/<RESOLVER-ID>
```

📷 _Placeholder:_
`![controld-device-endpoint](/img/jamfnow/controld-device-endpoint.png)`

***

## **Step 2 — Download or Generate a Control D .mobileconfig**

Use this XML template and replace `<RESOLVER-ID>`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
 "http://www.apple.com/DTDs/PropertyList-1.0.dtd">

<plist version="1.0">
<dict>
  <key>PayloadContent</key>
  <array>
    <dict>
      <key>DNSProtocol</key>
      <string>HTTPS</string>
      <key>ServerURL</key>
      <string>https://dns.controld.com/<RESOLVER-ID></string>
      <key>Identifier</key>
      <string>com.controld.dns</string>
      <key>PayloadIdentifier</key>
      <string>com.controld.dns.settings</string>
      <key>PayloadType</key>
      <string>com.apple.dnsSettings.managed</string>
      <key>PayloadUUID</key>
      <string>UUID-GOES-HERE</string>
      <key>PayloadVersion</key>
      <integer>1</integer>
    </dict>
  </array>
  <key>PayloadDisplayName</key>
  <string>Control D – DNS Enforcement</string>
  <key>PayloadIdentifier</key>
  <string>com.controld.dns.profile</string>
  <key>PayloadType</key>
  <string>Configuration</string>
  <key>PayloadUUID</key>
  <string>UUID-GOES-HERE-2</string>
  <key>PayloadVersion</key>
  <integer>1</integer>
</dict>
</plist>
```

***

## **Step 3 — Upload to Jamf Now**

In **Jamf Now Dashboard**:

1. Go to **Devices → Blueprints**
2. Select or create a Blueprint
3. Scroll to **Custom Profiles**
4. Click **Upload Custom Profile**
5. Upload your `.mobileconfig`

📷 _Placeholder:_
`![jamfnow-upload-profile](/img/jamfnow/jamfnow-upload-profile.png)`

***

## **Step 4 — Assign the Blueprint**

1. Go to **Devices**
2. Select your iOS/tvOS device
3. Apply the Blueprint containing the Control D profile

📷 _Placeholder:_
`![jamfnow-assign-blueprint](/img/jamfnow/jamfnow-assign-blueprint.png)`

***

## **Step 5 — Validate**

On the device:

❯ **Settings → General → VPN & Device Management → Configuration Profiles**
Look for:
**Control D – DNS Enforcement**

Then test:

```
https://verify.controld.com
```

📷 _Placeholder:_
`![verify-controld](/img/jamfnow/verify-controld.png)`

<br />
