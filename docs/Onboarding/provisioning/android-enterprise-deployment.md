---
title: Android Enterprise Deployment
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Use a single **provision token** to auto-create and enrol Android **Endpoints** at scale. Devices are managed by your MDM.

## Prerequisites

* Control D **Organization** account.
* **Provision token** from **Dashboard → Endpoints  →[Provision](https://controld.com/dashboard/provision)**.
* Android Enterprise devices enrolled in your **MDM**, with permission to push managed app configurations and enforce **Always-On VPN**.

***

## Step 1 — Sign in to Control D

Ensure you’re using an **Organization** account.

## Step 2 — Create a provision token

Go to **Dashboard → Endpoints → Provision** and generate a token (e.g., `org-v1-xxxx`). Keep it handy.

## Step 3 — Decide your device identifier

Pick a stable, unique value your MDM can template per device (e.g., device ID, serial, asset tag). This becomes the Control D **Endpoint name**.

## Step 4 — Add the Control D managed app to your MDM

Add the private/managed app to your Android Enterprise catalog.

## Step 5 — Create the managed app configuration

Add two keys:

* `provision_token` → your `org-v1-...` token
* `device_id` → your MDM’s per-device macro (e.g., MaaS360 `%deviceid%`)

**Template (managed\_config.xml)**

```xml
<restrictions xmlns:android="http://schemas.android.com/apk/res/android">
  <restriction
      android:key="provision_token"
      android:title="Control D Provision Token"
      android:restrictionType="string"
      android:defaultValue="" />
  <restriction
      android:key="device_id"
      android:title="Device ID"
      android:restrictionType="string"
      android:defaultValue="%deviceid%" />
</restrictions>
```

## Step 6 — Assign the configuration

Target the devices/groups you plan to enroll. Ensure the managed config is attached to the app assignment.

## Step 7 — Distribute the app silently

Push the app to devices. In Android Enterprise **Device Owner** mode, the install is silent and headless (visible in system settings, not the launcher).

## Step 8 — Enforce Always-On VPN

Create or update your security policy to set the Control D app as **Always-On VPN** and push it to the same devices.

## Step 9 — Confirm in the Control D dashboard

Open **Dashboard → Endpoints**. You should see a new **Endpoint** named after your `device_id`. Generate DNS traffic on the device and confirm activity under that **Endpoint's** Activity Log.