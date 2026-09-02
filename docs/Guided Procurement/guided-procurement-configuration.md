---
title: Configure Guided Procurement
deprecated: false
hidden: false
metadata:
  robots: index
---
Guided Procurement Basics


Before you start using the Guided Procurement API, we recommend you start by learning the Guided Procurement Basics. Understanding the concepts of the Guided Procurement module will help you:

Gain a better understanding of the procurement process.
Get the most out of the Airbase API and use it effectively.
Ensure you are following the appropriate procedures and meeting all necessary requirements.
Integrating your apps
The following concept diagram explains the high-level workflow of the API:

![](https://files.readme.io/ad1cd0a9cb4be103257c6c9a80402722c224399246e074718227ecfcd18a5097-image.png)

<br />

The procurement approval workflow integrated with a software of your choice follows a basic lifecycle that includes the following steps:

After an employee submits a purchase request on Airbase, the webhooks for the relevant events you subscribed to are triggered.
As a developer or an individual responsible for app integrations with the Airbase Guided Procurement API, you can use the webhook details to determine if the milestone is applicable to your use case.
Each webhook has a request ID and milestone ID- either of these can be used to get additional details for a request or a milestone.
Use the request details to initiate a workflow on your preferred software.
Wait for the workflow to complete on the software. After you receive the outcome of the workflow, you can approve or deny the specific milestone on Airbase.
The procurement workflow then proceeds to the next milestone(s).
Once all the milestones are fully approved, we inform the employee that their request is approved and the Virtual Card or Purchase Order has been created for them.
An example of the API in action with Asana
Let's say a team, like Legal, works primarily with a project management software like Asana. In this case, an end user would need to submit separate requests on Airbase and Asana for approval.

With Airbase APIs and webhooks, an integration can be built so that the end user only submits a request on Airbase.
Webhooks can then trigger an Asana workflow using the details captured in the Airbase request.
Once approved on Asana, Patch request APIs can be used to mark the request on Airbase as approved.
The above automation ensures:

The end user (spend owner/employee) need not log in to Airbase and Asana for a single purchase request.
The end user need not be trained (or remember) to always submit requests across multiple systems.
The legal team need not log in to Airbase for their legal reviews.
All stakeholders get real-time visibility into the status of the request on Airbase.
Note
Our design assumes that the request will be created on Airbase by the end-user (through the web app). We do not presently offer APIs for creating or submitting purchase requests.

Guided Procurement Configuration
The Guided Procurement workflow needs to be customized to capture the details the Legal team will need as part of the procurement approval process. Follow these steps:

Step 1: Sequence the milestone based on your business needs. If the Legal review needs to happen after the procurement approval, you can sequence the milestone appropriately using the Guided Procurement configuration. To do this go to Settings > Guided Procurement > Draft > Milestone Sequence.
Step 2: Customise the Airbase Guided Procurement workflow and create a milestone for the Legal review. Customize the form for this milestone to include all the details the legal team needs on the Asana workflow.
Step 3: Mark the legal team as the approver for this specific milestone.
Step 4: Use the Approval Matrix to define when the Legal review is required as part of the approval process. For example, Legal review is required only for software-related or contract-related purchase requests.
Step 5: Publish the configured workflow.
Configure the appropriate Webhooks
Once the Guided Procurement workflow is published, the next step is to subscribe to the appropriate webhook event(s) that can be used to initiate a workflow on Asana.

In this specific example, we will subscribe to the pending_approval webhook. This event is triggered for every milestone if the approval is pending on a specific milestone.
Within this webhook event, determine where the milestone name is Legal Review. This indicates that the milestone is pending approval from the Legal team.
Use the request ID in the event data to get the complete request. Details within the complete request can be used to create the Asana workflow details.
Once the workflow on the Asana is complete, the PATCH milestone API can be used to approve the Legal review milestone on behalf of the specific Legal team member.

Frequently Asked Questions (FAQs)
What’s the nature of authentication supported by Airbase?
Currently, we use token-based authentication for Airbase APIs.

Token-based authentication in APIs uses a unique token to authenticate and authorize users. Tokens are issued upon successful authentication and included in subsequent API requests.

They are short-lived, revocable, and provide a secure and efficient means of authentication and authorization for API communication.

How do I obtain the API access token?
An access token can be generated from the Airbase web app by going to Settings > Connections > Tokens & Webhooks.AT.png

![](https://files.readme.io/052cdad9d5e319e54c72a3e64d0ce102847b4fe41a9c782f6711a67d8a16dcae-image.png)