---
title: test
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
table_of_contents: true
---
This guide highlights the most important documentation for issuing banks and consumer payment service providers (consumer PSPs).

Follow the recommended path to understand the business flows, technical requirements, operational processes, and onboarding activities for integrating Wero.

***

## Step 1: Understand Wero fundamentals

Start with these pages to understand the main Wero capabilities, consent model, and mobile experience.

| Page                                                              | Priority    | Reading time | Purpose                                                                  |
| :---------------------------------------------------------------- | :---------- | :----------- | :----------------------------------------------------------------------- |
| [Concept and use cases: core features](doc:core-features)         | Essential   | 5 min        | Understand the main Wero capabilities and supported use cases.           |
| [Payment consent model](doc:consent-model-concept)                | Essential   | 15 min       | Learn how consumers give consent and how payment consent is represented. |
| [Mobile UX principles](doc:guidelines-for-mobile-user-experience) | Recommended | 5 min        | Apply the UX principles for Wero journeys in mobile banking apps.        |

**Total reading time: approximately 25 minutes**

***

## Step 2: Learn the payment journeys

Understand the actors and payment journeys that consumer PSPs support.

| Page                                                                                          | Priority  | Reading time | Purpose                                                                         |
| :-------------------------------------------------------------------------------------------- | :-------- | :----------- | :------------------------------------------------------------------------------ |
| [Conceptual overview of person-to-person payments](doc:person-to-person-payments)             | Essential | 15 min       | Understand the concepts and actors involved in person-to-person payments.       |
| [Conceptual overview of person-to-professional payments](doc:person-to-professional-payments) | Essential | 10 min       | Understand the concepts and actors involved in person-to-professional payments. |

**Total reading time: approximately 25 minutes**

***

## Step 3: Understand operational flows

Review the operational flows that are most relevant to consumer PSP implementations.

| Page                                                             | Priority    | Reading time | Purpose                                                                |
| :--------------------------------------------------------------- | :---------- | :----------- | :--------------------------------------------------------------------- |
| [Wallet management](doc:wallet-management)                       | Essential   | 5 min        | Follow the operational flows for managing Wero wallets.                |
| [Managing proxies](doc:proxy-management)                         | Recommended | 5 min        | Understand how proxy identifiers are managed and used.                 |
| [Sending and requesting money](doc:p2p-transaction-flows)        | Essential   | 5 min        | Follow the flows for sending and requesting person-to-person payments. |
| [Electronic commerce payments](doc:electronic-commerce-payments) | Recommended | 5 min        | Understand the operational flows for electronic commerce payments.     |

**Total reading time: approximately 20 minutes**

***

## Step 4: Prepare for onboarding and testing

Prepare the technical access and testing knowledge needed to progress your implementation.

| Page                                                                 | Priority  | Reading time | Purpose                                                                                |
| :------------------------------------------------------------------- | :-------- | :----------- | :------------------------------------------------------------------------------------- |
| [Technical onboarding](doc:technical-onboarding)                     | Essential | 5 min        | Prepare access, credentials, connectivity, and security material for EPI environments. |
| [Introduction to testing at EPI](doc:introduction-to-testing-at-epi) | Essential | 5 min        | Understand the testing stages and expectations for EPI implementations.                |

**Total reading time: approximately 10 minutes**

***

## Reference documentation

The following material is useful during implementation but is not typically required during the first onboarding phase.

### Data and architecture

| Page                                                              | Priority    | Reading time | Purpose                                                             |
| :---------------------------------------------------------------- | :---------- | :----------- | :------------------------------------------------------------------ |
| [Consumer data model](doc:consumer-data)                          | Recommended | 5 min        | Understand the consumer entities and data used by Wero.             |
| [Administration of EPI actors](doc:administration-of-wero-actors) | Reference   | 5 min        | Understand how EPI actors and their relationships are administered. |

### Settlement and risk

| Page                                                       | Priority    | Reading time | Purpose                                                         |
| :--------------------------------------------------------- | :---------- | :----------- | :-------------------------------------------------------------- |
| [Settlement through SCT Inst](doc:settlement-via-sct-inst) | Recommended | 5 min        | Understand how Wero payments are settled through SCT Inst.      |
| [Fraud management](doc:fraud-management)                   | Recommended | 5 min        | Review fraud-related concepts, responsibilities, and processes. |

***

## Common tasks

### I'm new to Wero

**Recommended reading: approximately 45 minutes**

1. [Concept and use cases: core features](doc:core-features).
2. [Payment consent model](doc:consent-model-concept).
3. [Conceptual overview of person-to-person payments](doc:person-to-person-payments).
4. [Conceptual overview of person-to-professional payments](doc:person-to-professional-payments).

### I'm designing the mobile experience

**Recommended reading: approximately 25 minutes**

1. [Mobile UX principles](doc:guidelines-for-mobile-user-experience).
2. [Payment consent model](doc:consent-model-concept).
3. [Wallet management](doc:wallet-management).

### I'm preparing technical integration

Start with [Technical onboarding](doc:technical-onboarding), then review the consumer data model and the operational flows relevant to your implementation.

### I'm preparing certification and go-live

Review [Technical onboarding](doc:technical-onboarding), [Introduction to testing at EPI](doc:introduction-to-testing-at-epi), [Fraud management](doc:fraud-management), and [Settlement through SCT Inst](doc:settlement-via-sct-inst) for an overview of certification and go-live preparation.

***

## Related pages

- [Your implementation journey](doc:your-implementation-journey)
- [Technical onboarding](doc:technical-onboarding)