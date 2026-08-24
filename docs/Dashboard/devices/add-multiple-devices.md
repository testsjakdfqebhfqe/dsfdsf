---
title: 'Org: Add Multiple Endpoints'
excerpt: >-
  Want to add hundreds of Endpoints in one go? There is a better way than
  pressing buttons.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
# Overview

If you need to add dozens (or hundreds) of Endpoints, click the `+` or `Create Endpoint` option, then you'll see this modal;


<Image src="https://files.readme.io/35d6de5955db5af062db8c756568a23ebfdcd95bec982deb5f372f03539a8f9d-add-multiple-endpoints.png" align="center" width="60%" />


Simply choose the **Endpoint Type** and then enter or paste a comma separated list of end-user emails or Endpoint names.

### Email End User

If you would like to create Endpoints for other users and have an email sent to them for onboarding, choose the `Create Provisioning Code` option in the top-right. Through this option, their device name would become the email username. ie. [james.tiberius.kirk@starfleet.com]() would become `james-tiberius-kirk`. **Additionally, the user will receive an email prompting them to[self-provision](doc:self-provisioning) the Device you just created.**

> 📘 Admin Rights Required
>
> If you're using this flow, the end user must have admin access to their machine to complete the onboarding. If they do not, you should use the Provisioning Codes flow, and use your RMM to do this on their behalf.

<br />
