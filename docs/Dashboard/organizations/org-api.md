---
title: API
excerpt: Generate tokens to manage your assets using an API.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is the API

The API section lets Organization admins and owners generate **and manage** access credentials for the [API](ref:get-started) to automate or script actions.

Using the API, you can do almost everything available in the Dashboard (the Dashboard uses the same API), including:

* View, create, and modify Profiles
* View, create, and modify Devices
* View and modify authorized IP lists

## Create a new API token

1. Go to **API** and click **+**.
2. Name the token and choose a type:

   * **Read** — View-only access
   * **Write** — View and modify data

Optionally, set **Allowed IPs** to restrict where the token can be used from.

## Edit an existing token (type and allowed IPs)

You can update a token’s scope and network restrictions at any time:

* In **API**, click the pencil icon next to a token to open the modal.
* Change the **Type** (Read/Write) and/or **Allowed IPs**.
* Save your changes.

> Tip: Tighten security by limiting tokens to the minimum necessary scope and adding specific allowed IPs for automation hosts.

![](https://files.readme.io/b7eae7c4a89aea8a130db5df2f6f46c0df67ca097de053aab5627b6d8d002606-image.png)

[API Documentation](/reference/get-started) is important reading if you wish to use the API.
