---
title: Connect an ERP
excerpt: >-
  This guide walks you through the onboarding steps required to connect an ERP
  to Paylocity for Finance. It covers establishing the connection, syncing ERP
  master data, and configuring GL account mappings so the integration is ready
  for transaction processing.
---
**1 - Connect Paylocity for Finance to the ERP during onboarding**

![](https://files.readme.io/90209227f3b9dab2a37fab7e74d39e0af89d5f8e6489d4c62fe80afaa55b790e-onboard_1.png)

- The customer initially configures the integration during their onboarding phase.

- An access token can be generated in the Paylocity for Finance web app as part of this process.

- The token is then stored in the ERP and used to authorize API communication between the two systems.

**2 - Push all ERP master data using a POST API call**

![](https://files.readme.io/aad2c24fd208882f7aa936f95d323ea6598679678761cf63b1d7b3d97fa26d70-onboard_2.png)

- Before any additional configuration, ERP master data must be pushed into Paylocity for Finance using the ERP master data APIs. This includes accounts, subsidiaries, currencies, tags, vendors, and employees.

- _Note: This step is mandatory and must be completed before transaction workflows can begin in Paylocity for Finance. To keep ERP master data in sync, we recommend running a scheduled job every 24 hours. Keeping this up to date reduces sync errors and ensures accurate accounting downstream._

**3 - Configure GL account mappings in Paylocity for Finance**

![](https://files.readme.io/65bcb708c1d97b38adc2e7dd27bfd800b12a2362bb79b6b429d1dddd0ffc464f-onboard_3.png)

- After the necessary ERP master data are created, the user completes the integration setup workflow in the Paylocity for Finance web app. This involves selecting the appropriate GL accounts to be used in spend workflows and transaction categorizations in Paylocity for Finance.

- _Note: These mappings can be viewed and updated at any time after onboarding._

<br />