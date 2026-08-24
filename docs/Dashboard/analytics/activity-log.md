---
title: Activity Log
excerpt: View historically made or real time DNS queries with additional metadata.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# What is Activity Log

This section allows you to view all DNS queries that were made historically, as well as view them in real time. 

![](https://files.readme.io/12918c198c014b6c7c543c0418977cae53ab37326bb97cf9a7aaaee18a5a7405-image.png)

# How to Use It

> 📘 Full Analytics
>
> In order to see DNS queries in the Activity Log, you need to enable "Full" [Analytics log level](doc:analytics-levels).

Simply navigate to the Analytics -> [Activity Log](https://controld.com/dashboard/activity-log) section, and choose an Endpoint you wish to monitor. From here, you can filter the data in multiple ways:

* **Date** - choose the date and time to view queries from the chosen time period 
* **Endpoints** - choose which Endpoint's data to view
* **Clients** (only available when an Endpoint is chosen) - choose which Client's query to view
* **Actions** - show queries based on a performed action (block, bypass, redirect)
* **Protocols** - show queries that used specific DNS protocols (Legacy, DNS-over-HTTPS, etc)
* **RCODEs** - show queries that resulted in a particular [return code](https://controld.com/blog/dns-return-codes/)
* **RTYPEs** - show queries that resulted in a particular [return type](https://en.wikipedia.org/wiki/List_of_DNS_record_types)
* **Filters** - show queries that were blocked by a specific Filter
* **Services** - show queries that were acted upon by a specific Service
* **Locations** - show queries that were redirected to a specific location

## Real Time Logging

![](https://files.readme.io/6e5b5c3e0c805967528186c3744e91069281fc6598f784259d75166647bfa150-image.png)

You can select Real-Time from the date selection dropdown to see DNS queries that are being made on a chosen Endpoint in real time.

> 📘 Real-Time Filtering
>
> In real-time mode, changing any filter - including the search field - starts a new real-time logging session. This clears the logs currently on screen, because the system only streams new DNS queries that match the updated filters. If you remove the search, you’ll see an empty list until new matching queries arrive. This is by design to improve performance in the browser.
>
> If you need to search past/older queries, switch to historical activity instead.

# Exporting Logs

If you've been asked by Control D Support to send Activity Logs or would like to export your logs for any other reason, there are two methods of doing so.

## Copy to Clipboard

![](https://files.readme.io/dd2ce6a3576407fbd79fb2167143ab32bae123fff372bb1e051a4341f46bc813-image.png)

At the top right of the log list you'll see this copy button. Click it to copy all the currently collected log results to your clipboard.

## Export Logs

![](https://files.readme.io/76895e49a8982fc862ad295ec6f4527e9482799041cef8e27ffa08c0923e49c2-image.png)

The button to the left of the copy button will export and download the currently collected logs in a convenient .csv format.
