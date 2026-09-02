---
title: Set up Guided Procurement webhooks
deprecated: false
hidden: false
metadata:
  robots: index
---
How to configure webhooks?
Introduction
Airbase offers webhooks that allow you to receive real-time updates about Guided Procurement request events that occur within our system. The webhook can be configured to send data to any URL of your choice, and it supports a variety of different event types.

Getting started with webhooks
To get started with creating a webhook,

Go to Dashbaord > Settings > Connections > Tokens and Webhooks > Webhooks.
Click Create Webhook.Create Webhook.png

![](https://files.readme.io/5c85f0a7bcf5b3ee0de6fbc670540128a71704baed7b4046c9defefdaa9cfe78-image.png)


Add the details on the Create Webhook pop-up.
Give the webhook a name, this can be anything that helps you identify the purpose of the webhook being setup.
Webhook POST URL: Add the URL where the notifications are sent to. Set up a webhook listening service on an automation tool like Zapier or Workato or create one from a custom server.
Select the events to be notified about. Find the 'Supported Event Types' listed below for the list of the events you can get notified about.

![](https://files.readme.io/ba8a97ef4376b254433327316197eb12f6f2caf031cca014cc0b64fffdabf919-image.png)

Screenshot 2026-02-24 at 16.04.45.png
Click Create.
Once you have completed the webhook configuration process, the webhook will be active and ready to start sending notifications to your specified URL.

Supported Event Types
The following event types are currently supported by the webhooks.

purchase.request.submitted Triggered when a new Guided Procurement request is submitted.
purchase.request.approved Triggered when the Guided Procurement request has approval on all the milestones and the complete request is marked as approved.
purchase.request.denied Triggered when any of the milestones are denied by the approver, and the complete Guided Procurement request is marked as denied.
purchase.request.archived Triggered when a created request is archived by the user.
purchase.request.active.milestones Milestones in the intake request are arranged in a hierarchical order. Approval happens from top to bottom. This event is triggered when a new level becomes active for approval. It can have one or more milestones.
purchase.request.comment.added Triggered whenever a new comment is added to the Guided Procurement request.
purchase.request.milestone.approved Triggered when the milestone is fully approved by all the approvers.
purchase.request.milestone.partially.approved Triggered when the milestone is approved but it still has pending approvers.
purchase.request.milestone.denied Triggered when a milestone is denied by the approver.
Webhook Payload
The webhook payload will be sent as a JSON object to your specified URL. The following fields will be included in the payload.

id: unique event id sent with each notification.
object: specified the type of object (for webhooks it will be “event”).
type: The type of event that triggered the webhook, as specified in the above section.
data: An object containing data related to the event.
Note: All the datetime fields are presented in the ISO format, the values are formatted according to ISO 8601 standards. For example,created_date, last_notified_time etc.

Examples
Guided Procurement request submission Event Type: purchase.request.submitted
Payload structure {
  "id": "fe81a810-6260-4b9d-8710-1ebcfd6a4925",
  "object": "event",
  "type": "purchase.request.submitted",
  "created_date": "2023-04-18T22:29:54.577844",
  "data": {
    "id": "10462ce8-b5f8-4130-ba77-9ccb14539339",
    "created_date": "2023-04-18T22:29:54.142881",
    "request_workflow_type": "INTAKE",
    "spend_mode": "purchase order",
    "status": "created",
    "primary_category": "Software Subscription",
    "secondary_category": "Developer Tools",
    "requested_amount": 123400,
    "requested_amount_currency": "USD",
    "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
    "vendor": {
      "name": "GitHub",
      "description": "GitHub provides code hosting services that allow developers to build software for open-source and private projects in organizations.",
      "website": "github.com",
      "vendor_type": "existing_vendor"
    },
    "requester": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "John@airbase.io"
    },
    "milestones": [
      [
        {
          "id": "34337024-bcc0-4726-922b-c5f6a1c66aa9",
          "created_date": "2023-04-18T22:29:54.577844",
          "name": "Department Approval",
          "status": "created"
        }
      ],
      [
        {
          "id": "8ddf00ea-14b5-4d67-a456-912e08158d12",
          "created_date": "2023-04-18T22:29:54.283305",
          "name": "Legal Review",
          "status": "created"
        },
        {
          "id": "b2552c71-5aad-4e1f-808a-e1b0649d1ef6",
          "created_date": "2023-04-18T22:29:54.399189",
          "name": "IT Approval",
          "status": "created"
        },
        {
          "id": "aa453fef-58c6-4260-ac3c-816c11de6335",
          "created_date": "2023-04-18T22:29:54.497527",
          "name": "Software and Services Procurement Approval",
          "status": "created"
        }
      ],
      [
        {
          "id": "110ce80e-8848-4f87-82e5-42e3c5b281ea",
          "created_date": "2023-04-18T22:29:54.204474",
          "name": "Finance & Accounting Approval",
          "status": "created"
        }
      ]
    ]
  }
}
milestones \*\*\*\*- The milestone data is structured as a 2D array that depicts the hierarchy of milestones from the top level to the bottom level.
data **→** id - Represents Guided Procurement request id.
data → vendor → vendor_type - it could be “existing_vendor” or “new_vendor” depending on selected vendor.
Guided Procurement request approved Event Type: purchase.request.approved
Payload structure {
    "id": "ec0b787c-08ed-4299-a3b0-7ab7ddbf5987",
    "object": "event",
    "type": "purchase.request.approved",
    "created_date": "2023-04-19T08:08:01.661938",
    "data": {
        "id": "ec8f5f30-abfd-4fb3-83bb-891ae7bc9611",
        "created_date": "2023-04-19T08:06:30.005518",
        "request_workflow_type": "INTAKE",
        "spend_mode": "purchase order",
        "status": "accepted",
        "primary_category": "Hire a contractor",
        "secondary_category": "Hire a contractor",
        "requested_amount": 12300,
        "requested_amount_currency": "USD",
        "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
        "vendor": {
        "name": "Apple",
        "description": "Apple is a multinational corporation that designs, manufactures, and markets consumer electronics, personal computers, and software.",
        "website": "apple.com",
        "vendor_type": "existing_vendor"
        },
        "requester": {
        "first_name": "John",
        "last_name": "Doe",
        "email": "John@airbase.io"
        },
        "milestones": [
        [
            {
            "id": "41f137c1-becf-44a3-a16a-4c3896579fe0",
            "created_date": "2023-04-19T08:06:30.232985",
            "name": "Department Approval",
            "status": "accepted"
            }
        ],
        [
            {
            "id": "9b608a66-1ef5-4051-a777-f6ca3ed5a1c8",
            "created_date": "2023-04-19T08:06:30.131282",
            "name": "Legal Review",
            "status": "accepted"
            }
        ],
        [
            {
            "id": "e8e0151e-c251-4d88-8114-d45bde3b7a87",
            "created_date": "2023-04-19T08:06:30.060760",
            "name": "Finance & Accounting Approval",
            "status": "accepted"
            }
        ]
        ]
    }
}
Guided Procurement request approved
-Event Type: purchase.request.approved - Payload structure

{
  "id": "ec0b787c-08ed-4299-a3b0-7ab7ddbf5987",
  "object": "event",
  "type": "purchase.request.approved",
  "created_date": "2023-04-19T08:08:01.661938",
  "data": {
    "id": "ec8f5f30-abfd-4fb3-83bb-891ae7bc9611",
    "created_date": "2023-04-19T08:06:30.005518",
    "request_workflow_type": "INTAKE",
    "spend_mode": "purchase order",
    "status": "accepted",
    "primary_category": "Hire a contractor",
    "secondary_category": "Hire a contractor",
    "requested_amount": 12300,
    "requested_amount_currency": "USD",
    "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
    "vendor": {
      "name": "Apple",
      "description": "Apple is a multinational corporation that designs, manufactures, and markets consumer electronics, personal computers, and software.",
      "website": "apple.com",
      "vendor_type": "existing_vendor"
    },
    "requester": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "John@airbase.io"
    },
    "milestones": [
      [
        {
          "id": "41f137c1-becf-44a3-a16a-4c3896579fe0",
          "created_date": "2023-04-19T08:06:30.232985",
          "name": "Department Approval",
          "status": "accepted"
        }
      ],
      [
        {
          "id": "9b608a66-1ef5-4051-a777-f6ca3ed5a1c8",
          "created_date": "2023-04-19T08:06:30.131282",
          "name": "Legal Review",
          "status": "accepted"
        }
      ],
      [
        {
          "id": "e8e0151e-c251-4d88-8114-d45bde3b7a87",
          "created_date": "2023-04-19T08:06:30.060760",
          "name": "Finance & Accounting Approval",
          "status": "accepted"
        }
      ]
    ]
  }
}
Guided Procurement request denied
Event Type: purchase.request.denied - Payload structure

{
  "id": "c088ae57-230c-453f-b85e-8bd268a8b020",
  "object": "event",
  "type": "purchase.request.denied",
  "created_date": "2023-04-19T06:36:09.366106",
  "data": {
    "id": "43543f31-f8b9-46e3-9a99-c720206514e9",
    "created_date": "2023-04-11T11:35:22.211333",
    "request_workflow_type": "INTAKE",
    "spend_mode": "purchase order",
    "status": "rejected",
    "primary_category": "Software Subscription",
    "secondary_category": "Developer Tools",
    "requested_amount": 1233400,
    "requested_amount_currency": "USD",
    "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
    "vendor": {
      "name": "123 Cheap Travel",
      "description": "123 Cheap Travel is a web based company.",
      "website": "123cheaptravel.co.uk",
      "vendor_type": "new_vendor"
    },
    "requester": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "John@airbase.io"
    },
    "milestones": [
      [
        {
          "id": "329a0f79-ff10-4082-b379-a23ddf44e366",
          "created_date": "2023-04-11T11:35:24.623460",
          "name": "Department Approval",
          "status": "accepted"
        }
      ],
      [
        {
          "id": "2a41c64c-4b74-4a24-8feb-9e6ec1e7ef81",
          "created_date": "2023-04-11T11:35:22.877423",
          "name": "Legal Review",
          "status": "created"
        },
        {
          "id": "deb56f92-2e37-45a1-906b-9833c846f181",
          "created_date": "2023-04-11T11:35:23.542119",
          "name": "IT Approval",
          "status": "rejected"
        },
        {
          "id": "2d98a9c8-d86b-4e8a-9eb5-59e262bc4d29",
          "created_date": "2023-04-11T11:35:24.066193",
          "name": "Software and Services Procurement Approval",
          "status": "created"
        }
      ],
      [
        {
          "id": "7e7b068f-1a4a-4433-be03-9fb6abf46d5c",
          "created_date": "2023-04-11T11:35:22.480631",
          "name": "Finance & Accounting Approval",
          "status": "created"
        }
      ]
    ]
  }
}
Guided Procurement request archived
Event Type: purchase.request.archived - Payload structure

{
  "id": "4d231f76-00cb-44b1-b7e7-c3ded83b0b69",
  "object": "event",
  "type": "purchase.request.archived",
  "created_date": "2023-04-19T06:33:50.267465",
  "data": {
    "id": "10462ce8-b5f8-4130-ba77-9ccb14539339",
    "created_date": "2023-04-18T22:29:54.142881",
    "request_workflow_type": "INTAKE",
    "spend_mode": "purchase order",
    "status": "archived",
    "primary_category": "Software Subscription",
    "secondary_category": "Developer Tools",
    "requested_amount": 123400,
    "requested_amount_currency": "USD",
    "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
    "vendor": {
      "name": "GitHub",
      "description": "GitHub provides code hosting services that allow developers to build software for open-source and private projects in organizations.",
      "website": "github.com",
      "vendor_type": "existing_vendor"
    },
    "requester": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "John@airbase.io"
    },
    "milestones": [
      [
        {
          "id": "34337024-bcc0-4726-922b-c5f6a1c66aa9",
          "created_date": "2023-04-18T22:29:54.577844",
          "name": "Department Approval",
          "status": "accepted"
        }
      ],
      [
        {
          "id": "8ddf00ea-14b5-4d67-a456-912e08158d12",
          "created_date": "2023-04-18T22:29:54.283305",
          "name": "Legal Review",
          "status": "created"
        },
        {
          "id": "b2552c71-5aad-4e1f-808a-e1b0649d1ef6",
          "created_date": "2023-04-18T22:29:54.399189",
          "name": "IT Approval",
          "status": "accepted"
        },
        {
          "id": "aa453fef-58c6-4260-ac3c-816c11de6335",
          "created_date": "2023-04-18T22:29:54.497527",
          "name": "Software and Services Procurement Approval",
          "status": "accepted"
        }
      ],
      [
        {
          "id": "110ce80e-8848-4f87-82e5-42e3c5b281ea",
          "created_date": "2023-04-18T22:29:54.204474",
          "name": "Finance & Accounting Approval",
          "status": "created"
        }
      ]
    ],
    "archived_by": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "John@airbase.io",
      "archived_at": "2023-04-19T06:33:50.139190"
    }
  }
}
-archived_by represents the user who archived the request.

Guided Procurement active milestones
Event Type: purchase.request.active.milestones - Payload structure

{
  "id": "021c6cab-dfb7-40aa-a83d-ca4e2d3d2b2a",
  "object": "event",
  "type": "purchase.request.active.milestones",
  "created_date": "2023-04-24T16:00:58.412792",
  "data": {
    "id": "None",
    "created_date": "2023-04-19T09:11:30.135880",
    "request_workflow_type": "INTAKE",
    "spend_mode": "recurring virtual card",
    "status": "created",
    "primary_category": "Employee Benefits",
    "secondary_category": "Swag",
    "requested_amount": 9000,
    "requested_amount_currency": "USD",
    "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
    "vendor": {
      "name": "FreshBake",
      "description": null,
      "website": "",
      "vendor_type": "existing_vendor"
    },
    "requester": {
      "first_name": "Chetanya",
      "last_name": "Shrimali",
      "email": "chetanya.shrimali@airbase.io"
    },
    "active_milestones": [
      {
        "id": "94790879-51f2-458a-8f87-d31522344c36",
        "created_date": "2023-04-19T09:11:30.216810",
        "name": "Department Approval",
        "status": "created"
      },
      {
        "id": "a20e4c66-14d7-406d-b054-7ab2a1c2e5a3",
        "created_date": "2023-04-20T14:33:04.387024",
        "name": "Department Approval",
        "status": "created"
      },
      {
        "id": "db7b4dc0-c7c3-487d-a256-e04ca2d61ee4",
        "created_date": "2023-04-20T14:33:22.939658",
        "name": "New Milestone",
        "status": "created"
      }
    ]
  }
}
active_milestones It shows the currently active milestones for approval.
Guided Procurement comment notification
Event Type: purchase.request.comment.added
Payload structure

{
  "id": "8f22b399-fe1c-4799-8781-deb831488143",
  "object": "event",
  "type": "purchase.request.comment.added",
  "created_date": "2023-04-19T05:53:12.014725",
  "data": {
    "request": {
      "id": "10462ce8-b5f8-4130-ba77-9ccb14539339",
      "created_date": "2023-04-18T22:29:54.142881",
      "request_workflow_type": "INTAKE",
      "spend_mode": "purchase order",
      "status": "created",
      "primary_category": "Software Subscription",
      "secondary_category": "Developer Tools",
      "requested_amount": 123400,
      "requested_amount_currency": "USD",
      "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
      "vendor": {
        "name": "GitHub",
        "description": "GitHub provides code hosting services that allow developers to build software for open-source and private projects in organizations.",
        "website": "github.com",
        "vendor_type": "existing_vendor"
      },
      "requester": {
        "first_name": "John",
        "last_name": "Doe",
        "email": "John@airbase.io"
      }
    },
    "comment": {
      "created_date": "2023-04-19T05:53:10.656394",
      "body": "hello @Intake group #2 (all-member-non-seq) test comment!",
      "added_by": {
        "first_name": "John",
        "last_name": "Doe",
        "email": "John@airbase.io"
      }
    }
  }
}
comment → body represents a comment by the user. Tagged users or groups are represented as a string.
comment → added_by represents the user who made the comment.
Milestone approved Event Type: purchase.request.milestone.approved
Payload structure {
  "id": "604a3507-7742-485f-8261-5f6e8970e035",
  "object": "event",
  "type": "purchase.request.milestone.approved",
  "created_date": "2023-04-19T06:08:11.003567",
  "data": {
    "id": "b2552c71-5aad-4e1f-808a-e1b0649d1ef6",
    "created_date": "2023-04-18T22:29:54.399189",
    "name": "IT Approval",
    "status": "accepted",
    "request": {
      "id": "10462ce8-b5f8-4130-ba77-9ccb14539339",
      "created_date": "2023-04-18T22:29:54.142881",
      "request_workflow_type": "INTAKE",
      "spend_mode": "purchase order",
      "status": "created",
      "primary_category": "Software Subscription",
      "secondary_category": "Developer Tools",
      "requested_amount": 123400,
      "requested_amount_currency": "USD",
      "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
      "vendor": {
        "name": "GitHub",
        "description": "GitHub provides code hosting services that allow developers to build software for open-source and private projects in organizations.",
        "website": "github.com",
        "vendor_type": "existing_vendor"
      },
      "requester": {
        "first_name": "John",
        "last_name": "Doe",
        "email": "John@airbase.io"
      }
    },
    "pending_on": {},
    "approval_chain": [
      {
        "type": "individual",
        "details": {
          "status": "approved",
          "last_notified_time": "2023-04-19T06:08:00.934621",
          "approver": {
            "first_name": "John",
            "last_name": "Doe",
            "email": "John@airbase.io"
          }
        }
      }
    ],
    "milestone_data": [
      {
        "name": "IT Review",
        "description": "This information will help the IT team perform proper software or hardware maintenance. For any questions or clarifications, please reach out directly to the IT team.",
        "elements": [
          {
            "type": "TEXT",
            "label": "Name of the Application or Service",
            "user_input": null,
            "is_standard": false,
            "field_id": "b25d8944-77aa-4a4d-8b90-1604e492eeb6"
          },
          {
            "type": "TEXT",
            "label": "Description of the Application or Service",
            "user_input": null,
            "is_standard": false,
            "field_id": "d9a449a2-e4eb-473e-8e16-a126778601d8"
          },
          {
            "type": "TEXT",
            "label": "How will this tool will be used?",
            "user_input": null,
            "is_standard": false,
            "field_id": "aec8e1c5-6008-48c7-8b56-c43c844cbeef"
          },
          {
            "type": "TEXT",
            "label": "What tool was previously being used and why is a new one needed?",
            "user_input": null,
            "is_standard": false,
            "field_id": "514db8e4-5e2c-45b4-90c1-a03da5b6f8ad"
          },
          {
            "type": "MULTI_SELECT",
            "label": "Which departments will be using this tool?",
            "user_input": "Sales, Engineering",
            "is_standard": false,
            "field_id": "4042d6ce-9222-44e8-891d-e9701ed591b4"
          },
          {
            "type": "RADIO_SELECT",
            "label": "Does the tool support Single Assertion Markup Language (SAML) authentication (e.g. SSO via Okta)?",
            "user_input": "I don’t know",
            "is_standard": false,
            "field_id": "1e77a3e1-73b8-4deb-817c-7275b66a3930"
          },
          {
            "type": "PERSON",
            "label": "Primary Business Owner",
            "user_input": {
              "first_name": "Jason",
              "last_name": "Blake",
              "email": "jason.blake@airbase.io"
            },
            "is_standard": false,
            "field_id": "e9840cf4-9a13-4b9a-96cb-69e52ce7ebdb"
          },
          {
            "type": "PERSON",
            "label": "Secondary Business Owner",
            "user_input": {
              "first_name": "William",
              "last_name": "Tell",
              "email": "william@airbase.io"
            },
            "is_standard": false,
            "field_id": "c1e498fb-60ab-4f94-aff8-e129da6a2317"
          },
          {
            "type": "RADIO_SELECT",
            "label": "Has the vendor completed the Vendor Assessment Form?",
            "user_input": "Yes",
            "is_standard": false,
            "field_id": "c62df0d0-b3a1-443c-895d-309d3b6ef574"
          },
          {
            "type": "URL",
            "label": "Link to Completed Vendor Assessment Form",
            "user_input": null,
            "is_standard": false,
            "field_id": "f387f7f9-4855-4304-b02e-9167c5fc5927"
          }
        ]
      }
    ],
    "approved_by": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "john@airbase.io",
      "approved_at": "2023-04-19T06:08:10.742448"
    }
  }
}
approved_by represents the final approver.
Milestone partially approved Event Type: purchase.request.milestone.partially.approved Payload structure {
  "id": "e3d7c5b6-02ed-48ec-9c78-69b217194883",
  "object": "event",
  "type": "purchase.request.milestone.partially.approved",
  "created_date": "2023-04-19T06:25:39.917930",
  "data": {
    "id": "fbbdbabb-90c9-4c96-acc9-0cc11265ed55",
    "created_date": "2023-04-19T06:11:38.011009",
    "name": "IT Approval",
    "status": "created",
    "request": {
      "id": "ccb3e1ce-b4bb-40e7-93b5-28681ff1b40a",
      "created_date": "2023-04-19T06:11:37.737935",
      "request_workflow_type": "INTAKE",
      "spend_mode": "purchase order",
      "status": "created",
      "primary_category": "Software Subscription",
      "secondary_category": "Developer Tools",
      "requested_amount": 123400,
      "requested_amount_currency": "USD",
      "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
      "vendor": {
        "name": "GitHub",
        "description": "GitHub provides code hosting services that allow developers to build software for open-source and private projects in organizations.",
        "website": "github.com",
        "vendor_type": "existing_vendor"
      },
      "requester": {
        "first_name": "Mrinal",
        "last_name": "Sinha",
        "email": "mrinal@airbase.io"
      }
    },
    "pending_on": {
      "type": "individual",
      "details": {
        "status": "pending",
        "last_notified_time": "2023-04-19T06:25:39.806694",
        "approver": {
          "first_name": "Rishi",
          "last_name": "Yadav",
          "email": "rishi@airbase.io"
        }
      }
    },
    "approval_chain": [
      {
        "type": "individual",
        "details": {
          "status": "approved",
          "last_notified_time": "2023-04-19T06:25:20.912892",
          "approver": {
            "first_name": "Mrinal",
            "last_name": "Sinha",
            "email": "mrinal@airbase.io"
          }
        }
      },
      {
        "type": "individual",
        "details": {
          "status": "pending",
          "last_notified_time": "2023-04-19T06:25:39.806694",
          "approver": {
            "first_name": "Rishi",
            "last_name": "Yadav",
            "email": "rishi@airbase.io"
          }
        }
      },
      {
        "type": "group",
        "details": {
          "members": [
            {
              "first_name": "Bela",
              "last_name": "Yatco",
              "email": "bela@airbase.io"
            },
            {
              "first_name": "Dilip",
              "last_name": "Kumar Pulla",
              "email": "dilip.kumar@airbase.io"
            }
          ],
          "last_notified_user": {
            "first_name": "Dilip",
            "last_name": "Kumar Pulla",
            "email": "dilip.kumar@airbase.io"
          },
          "last_approved_user": {},
          "last_notified_time": "2023-04-19T06:15:21.640953",
          "status": "pending"
        }
      }
    ],
    "milestone_data": [
      {
        "name": "IT Review",
        "description": "This information will help the IT team perform proper software or hardware maintenance. For any questions or clarifications, please reach out directly to the IT team.",
        "elements": [
          {
            "type": "TEXT",
            "label": "Name of the Application or Service",
            "user_input": null,
            "is_standard": false,
            "field_id": "b25d8944-77aa-4a4d-8b90-1604e492eeb6"
          },
          {
            "type": "TEXT",
            "label": "Description of the Application or Service",
            "user_input": null,
            "is_standard": false,
            "field_id": "d9a449a2-e4eb-473e-8e16-a126778601d8"
          },
          {
            "type": "TEXT",
            "label": "How will this tool will be used?",
            "user_input": null,
            "is_standard": false,
            "field_id": "aec8e1c5-6008-48c7-8b56-c43c844cbeef"
          },
          {
            "type": "TEXT",
            "label": "What tool was previously being used and why is a new one needed?",
            "user_input": null,
            "is_standard": false,
            "field_id": "514db8e4-5e2c-45b4-90c1-a03da5b6f8ad"
          },
          {
            "type": "MULTI_SELECT",
            "label": "Which departments will be using this tool?",
            "user_input": "Sales, Product",
            "is_standard": false,
            "field_id": "4042d6ce-9222-44e8-891d-e9701ed591b4"
          },
          {
            "type": "RADIO_SELECT",
            "label": "Does the tool support Single Assertion Markup Language (SAML) authentication (e.g. SSO via Okta)?",
            "user_input": null,
            "is_standard": false,
            "field_id": "1e77a3e1-73b8-4deb-817c-7275b66a3930"
          },
          {
            "type": "PERSON",
            "label": "Primary Business Owner",
            "user_input": null,
            "is_standard": false,
            "field_id": "e9840cf4-9a13-4b9a-96cb-69e52ce7ebdb"
          },
          {
            "type": "PERSON",
            "label": "Secondary Business Owner",
            "user_input": null,
            "is_standard": false,
            "field_id": "c1e498fb-60ab-4f94-aff8-e129da6a2317"
          },
          {
            "type": "RADIO_SELECT",
            "label": "Has the vendor completed the Vendor Assessment Form?",
            "user_input": null,
            "is_standard": false,
            "field_id": "c62df0d0-b3a1-443c-895d-309d3b6ef574"
          },
          {
            "type": "URL",
            "label": "Link to Completed Vendor Assessment Form",
            "user_input": null,
            "is_standard": false,
            "field_id": "f387f7f9-4855-4304-b02e-9167c5fc5927"
          }
        ]
      }
    ],
    "approved_by": {
      "first_name": "Mrinal",
      "last_name": "Sinha",
      "email": "mrinal@airbase.io",
      "approved_at": "2023-04-19T06:25:11.641240"
    }
  }
}
Milestone denied
Event Type: purchase.request.milestone.denied

Payload structure

{
  "id": "2141cf2f-7f4f-4e5e-9364-dbea4b8a4647",
  "object": "event",
  "type": "purchase.request.milestone.denied",
  "created_date": "2023-04-19T06:36:07.796871",
  "data": {
    "id": "deb56f92-2e37-45a1-906b-9833c846f181",
    "created_date": "2023-04-11T11:35:23.542119",
    "name": "IT Approval",
    "status": "rejected",
    "request": {
      "id": "43543f31-f8b9-46e3-9a99-c720206514e9",
      "created_date": "2023-04-11T11:35:22.211333",
      "request_workflow_type": "INTAKE",
      "spend_mode": "purchase order",
      "status": "rejected",
      "primary_category": "Software Subscription",
      "secondary_category": "Developer Tools",
      "requested_amount": 1233400,
      "requested_amount_currency": "USD",
      "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
      "vendor": {
        "name": "123 Cheap Travel",
        "description": "123 Cheap Travel is a web based company.",
        "website": "123cheaptravel.co.uk",
        "vendor_type": "new_vendor"
      },
      "requester": {
        "first_name": "Mrinal",
        "last_name": "Sinha",
        "email": "mrinal@airbase.io"
      }
    },
    "pending_on": {},
    "approval_chain": [
      {
        "type": "individual",
        "details": {
          "status": "denied",
          "last_notified_time": "2023-04-19T06:35:38.950919",
          "approver": {
            "first_name": "Mrinal",
            "last_name": "Sinha",
            "email": "mrinal@airbase.io"
          }
        }
      },
      {
        "type": "group",
        "details": {
          "members": [
            {
              "first_name": "Bela",
              "last_name": "Yatco",
              "email": "bela@airbase.io"
            },
            {
              "first_name": "Dilip",
              "last_name": "Kumar Pulla",
              "email": "dilip.kumar@airbase.io"
            }
          ],
          "last_notified_user": {
            "first_name": "Dilip",
            "last_name": "Kumar Pulla",
            "email": "dilip.kumar@airbase.io"
          },
          "last_approved_user": {},
          "last_notified_time": "2023-04-11T11:39:20.359845",
          "status": "pending"
        }
      }
    ],
    "milestone_data": [
      {
        "name": "IT Review",
        "description": "This information will help the IT team perform proper software or hardware maintenance. For any questions or clarifications, please reach out directly to the IT team.",
        "elements": [
          {
            "type": "TEXT",
            "label": "Name of the Application or Service",
            "user_input": null,
            "is_standard": false,
            "field_id": "b25d8944-77aa-4a4d-8b90-1604e492eeb6"
          },
          {
            "type": "TEXT",
            "label": "Description of the Application or Service",
            "user_input": null,
            "is_standard": false,
            "field_id": "d9a449a2-e4eb-473e-8e16-a126778601d8"
          },
          {
            "type": "TEXT",
            "label": "How will this tool will be used?",
            "user_input": null,
            "is_standard": false,
            "field_id": "aec8e1c5-6008-48c7-8b56-c43c844cbeef"
          },
          {
            "type": "TEXT",
            "label": "What tool was previously being used and why is a new one needed?",
            "user_input": null,
            "is_standard": false,
            "field_id": "514db8e4-5e2c-45b4-90c1-a03da5b6f8ad"
          },
          {
            "type": "MULTI_SELECT",
            "label": "Which departments will be using this tool?",
            "user_input": "Sales",
            "is_standard": false,
            "field_id": "4042d6ce-9222-44e8-891d-e9701ed591b4"
          },
          {
            "type": "RADIO_SELECT",
            "label": "Does the tool support Single Assertion Markup Language (SAML) authentication (e.g. SSO via Okta)?",
            "user_input": null,
            "is_standard": false,
            "field_id": "1e77a3e1-73b8-4deb-817c-7275b66a3930"
          },
          {
            "type": "PERSON",
            "label": "Primary Business Owner",
            "user_input": null,
            "is_standard": false,
            "field_id": "e9840cf4-9a13-4b9a-96cb-69e52ce7ebdb"
          },
          {
            "type": "PERSON",
            "label": "Secondary Business Owner",
            "user_input": null,
            "is_standard": false,
            "field_id": "c1e498fb-60ab-4f94-aff8-e129da6a2317"
          },
          {
            "type": "RADIO_SELECT",
            "label": "Has the vendor completed the Vendor Assessment Form?",
            "user_input": null,
            "is_standard": false,
            "field_id": "c62df0d0-b3a1-443c-895d-309d3b6ef574"
          },
          {
            "type": "URL",
            "label": "Link to Completed Vendor Assessment Form",
            "user_input": null,
            "is_standard": false,
            "field_id": "f387f7f9-4855-4304-b02e-9167c5fc5927"
          }
        ]
      }
    ],
    "denied_by": {
      "first_name": "Mrinal",
      "last_name": "Sinha",
      "email": "mrinal@airbase.io",
      "reason": "Test denying",
      "denied_at": "2023-04-19T06:35:51.927123"
    }
  }
}

Vendor Webhooks
Vendor Rename
Triggered when a new vendor created through a purchase request has been renamed.

Note: Only a new vendor which is pending for approval can be renamed.

Type: purchase.request.vendor.renamed

Payload

The payload contains only vendor information on a purchase request.

{
    "id": "ee610924-6664-455f-b6cb-cf5d62f449e9",
    "object": "event",
    "type": "purchase.request.vendor.renamed",
    "created_date": "2024-07-22T08:59:24.670091",
    "data": {
        "object_id": "2ee2593b-0a3e-4702-9bbc-9656338884f7",
        "object_type": "guided_procurement_request",
        "created_date": "2024-07-20T12:55:06.042018",
        "vendor": {
            "name": "Google",
            "description": "Google LLC is an American multinational technology company focusing on search engine technology, online advertising, cloud computing, computer software, quantum computing, e-commerce, artificial intelligence, and consumer electronics",
            "website": "google.com",
            "vendor_type": "new_vendor",
            "status": "pending"
        }
    }
}
status: current status of the vendor.

Vendor Approval
Triggered when vendor approval milestone of a purchase request has been approved. If the vendor approval milestone of a purchase request has been approved, the vendor will be added to the vendor catalog even if the associated purchase request has been archived/rejected.

Type: purchase.request.vendor.approved

{
    "id": "707a19de-ee6b-4205-b4ef-787a50c1e7b9",
    "object": "event",
    "type": "purchase.request.vendor.approved",
    "created_date": "2024-07-22T08:58:35.301929",
    "data": {
        "object_id": "2ee2593b-0a3e-4702-9bbc-9656338884f7",
        "object_type": "guided_procurement_request",
        "created_date": "2024-07-20T12:55:06.042018",
        "vendor": {
            "name": "Google",
            "description": "Google LLC is an American multinational technology company focusing on search engine technology, online advertising, cloud computing, computer software, quantum computing, e-commerce, artificial intelligence, and consumer electronics",
            "website": "google.com",
            "vendor_type": "new_vendor",
            "status": "accepted"
        }
    }
}
Purchase request update
Triggered when purchase request has been updated after submitting the request.

Type: purchase.request.updated

Payload

Payload is the same as other purchase request webhooks.

{
    "id": "0d9d6b56-4053-4ab4-a5ab-5dd984f689ef",
    "object": "event",
    "type": "purchase.request.updated",
    "created_date": "2024-07-22T09:05:17.613551",
    "data": {
        "object_id": "2ee2593b-0a3e-4702-9bbc-9656338884f7",
        "object_type": "guided_procurement_request",
        "created_date": "2024-07-20T12:55:06.042018",
        "request_workflow_type": "INTAKE",
        "spend_mode": null,
        "status": "draft",
        "primary_category": "Software Subscription",
        "secondary_category": "Developer Tools",
        "requested_amount": 12300,
        "requested_amount_currency": "USD",
        "request_url": "https://dashboard.airbase.io/requests/intake-requests/created/1234/summary/",
        "vendor": {
            "name": "Google",
            "description": "Google LLC is an American multinational technology company focusing on search engine technology, online advertising, cloud computing, computer software, quantum computing, e-commerce, artificial intelligence, and consumer electronics",
            "website": "google.com",
            "vendor_type": "existing_vendor",
            "status": "pending"
        },
        "description": "ese",
        "requester": {
            "first_name": "Mrinal",
            "last_name": "Sinha",
            "email": "mrinal@airbase.io"
        },
        "custom_sections": [
            {
                "name": "Primary Information",
                "description": null,
                "elements": [
                    {
                        "type": "SPEND_CATEGORY_SELECT",
                        "label": "Spend Category Selection",
                        "user_input": null,
                        "is_standard": true,
                        "field_id": null
                    }
                ]
            },
            {
                "name": "Vendor & Budget Details",
                "description": null,
                "elements": [
                    {
                        "type": "AMOUNT",
                        "label": "Welcome to Airbase Staging's purchase request workflow! Throughout this form, we’ll be asking you to provide information about your intended purchase, along with other details required by relevant approving teams in the organization.",
                        "user_input": null,
                        "is_standard": true,
                        "field_id": null
                    },
                    {
                        "type": "REQUEST_DESCRIPTION",
                        "label": "Provide a short description of the problem you plan to address with this purchase",
                        "user_input": null,
                        "is_standard": true,
                        "field_id": null
                    },
                    {
                        "type": "ATTACHMENT",
                        "label": "Attachment of draft contract (if available)",
                        "files": [],
                        "is_standard": false,
                        "field_id": "ea76aa94-6a64-4938-99a7-67b95a987c03"
                    }
                ]
            }
        ],
        "milestones": [
            [
                {
                    "object_id": "d69d13d5-9448-473b-8186-5c64bed992e9",
                    "object_type": "milestone",
                    "created_date": "2024-07-20T12:55:06.206265",
                    "name": "Finance & Accounting Approval",
                    "status": "initialized"
                }
            ]
        ]
    }
}
About API Security
The webhook payload is sent over HTTPS to ensure that it is transmitted securely. In addition, we recommend that you verify the payload signature to ensure that it has not been tampered with. The signature is calculated using the HMAC-SHA256 algorithm and is included in the x-airbase-hmac-sha256 header.