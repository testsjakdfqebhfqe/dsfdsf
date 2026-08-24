---
title: Analytics
excerpt: View your historical activity.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What are Analytics

The Analytics feature allows you to gain insights on your historical browsing activity. The [Analytics Dashboard](https://controld.com/dashboard/statistics) has several sections:

1. **[Statistics](/docs/statistics)** - Shows a summary of your usage patterns and general trends
2. **[Activity Log](/docs/activity-log)** - Shows exact queries that were made and additional metadata.

<Image border={false} src="https://files.readme.io/17346c05eb493192dd63305e5514ccd8c9462fff5190ad37b56feaef37132871-image.png" />

# How to Enable Analytics

To enable Analytics, simply edit an Endpoint and choose one of the [Analytics Levels](/docs/analytics-levels). Then head over to the Analytics Dashboard and view the stats.

# Data Storage Rules

## Storage Region

In Preferences -> Account, you can select a Storage Region. This is where your data will be physically stored should you choose to enable the Analytics feature.

## Granular Data

The most granular data stored by Control D in any circumstance is kept for a maximum of one month. This is only the case when you have selected Full Analytics for the Device in question. In this case, Control D stores the following information about each of the DNS queries made against your Control D Device’s resolvers:

* Domain name
* Date and time of query
* Protocol used
* DNS return code
* Type of record
* Action taken (blocked, bypassed, or redirected)
* Reason for action taken (Filter, Service, Custom Rule, Default Rule)
* Context for reason (which specific Filter, Service, Custom Rule, and if redirected, which location or IP it was redirected via)
* Source IP address
* Destination IP address/es

This data is what makes the Activity Log possible. We never store it unless you choose to select Full Analytics. It is impossible to see your browsing data in the Activity Log unless Full Analytics is selected for the Device being viewed for this exact reason: we respect you and your privacy.

## Domain Data

We keep all other data for Analytics for a maximum of 1 year, or until you delete it.

## Data Retention Summary

### Raw Query Logs

Raw DNS query logs are stored for **1 month**.

### Statistics

Other statistics data is stored for **1 year**.

## Delete Analytics Data

You can delete your Analytics data across every Device for the currently selected storage region in Preferences. Simply click the Delete button here:

<Image border={false} src="https://files.readme.io/8f3f90427038d40e250b15f6806f30e92cab2b6df2806f9b3e92c276ebcd31e0-image.png" />

<br />

> 🚧 It may take up to 48 hours to completely delete your data.
