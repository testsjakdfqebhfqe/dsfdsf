---
title: Paylocity for Finance APIs overview
excerpt: >-
  Explore the APIs available for ERP integration, financial reporting, Guided
  Procurement, and event-driven workflows.
deprecated: false
hidden: false
metadata:
  robots: index
---
After a user has been approved for an unsecured personal loan, they're taken to their loan dashboard the next time they log into the white label app. Here, they can view their outstanding balance, make extra loan payments, settle their loan early and generally manage their loan.

This page covers the actions a user can take specifically on an unsecured personal loan account. See [this page](https://docs.nwboxed.com/natwest-boxed-docs/docs/manage-account#/) for more information on the general actions users can take on their account.

<SupermartBrandingInfo />

## The loan dashboard

The loan dashboard is the first screen a user will see after logging into the NatWest Boxed white label app, and contains a summary of their unsecured personal loan. The user can also [make an extra payment](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#make-an-extra-payment) from this screen.


<Image src="https://files.readme.io/3dcd8a17d2963903c5a612b989aa17e1b128c774f33468f7953c3be544243dab-image.png" align="center" width="200px" />


<br />

### Loan balance

The outstanding balance to be repaid is recorded at the top of the screen. This is the notional balance calculated in real-time as:

> Notional balance = (Principal amount + capitalised interest) - the principal part of all repayments made to date

Capitalised interest is applied on the first calendar day of each month.

### Next payment

Details of the next payment are recorded below the outstanding balance and **Make extra payment** button:

* Date of next payment
* Next payment amount (including interest)

### Payment history

The user's payment history is recorded at the bottom of the screen. Regular payments are recorded as _Monthly payment_ and any extra payments are recorded as _Additional payment_.

<br />

## Menu actions

On a smart phone, the following actions are performed by selecting the menu icon&#x20;


<Image src="https://files.readme.io/c39652f2ab5770e8de15ea5d428ddeb5bf51188c18eed6275c758f09b08bbc0c-image.png" alt="menu icon" width="15px" />


&#x20;in the upper left corner of the screen. On a desktop web browser, the actions are found in a sidebar on the left of the screen.

Each action is detailed below.

* [Edit repayment details](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#edit-repayment-details)
* [Make an extra payment](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#make-an-extra-payment)
* [Request early settlement](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#request-early-settlement)
* [Withdraw from loan agreement](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#withdraw-from-loan-agreement)
* [View annual statement](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#view-annual-statements)s


<Image src="https://files.readme.io/66db2dfc40d730a0a3ba63e1a7d3ff5b75fb30e38101799e9e47b09a2ea67e91-UPL_Manage_Account_Menu_March2026.png" align="center" width="900px" />


<br />

### Edit repayment details

The user needs to contact NatWest Boxed to change the bank account their repayments are collected from, or the date repayments are made. To do so:

1. The user selects the menu icon&#x20;


   <Image src="https://files.readme.io/c39652f2ab5770e8de15ea5d428ddeb5bf51188c18eed6275c758f09b08bbc0c-image.png" alt="menu icon" width="15px" />


   &#x20;in the top-left of the screen, then selects **Repayment details**.
2. The user selects **Contact us** to get in touch with the NatWest Boxed support team.


<Image src="https://files.readme.io/cb274a102a67642b972bfaa6a0dfd4aa13397abc90e2b3e417faa51b0423419b-image.png" align="center" width="200px" />


<br />

### Make an extra payment

The user can make extra payments towards their loan at any time, and without any limits.

They'll be charged interest based on the payment amount, which is 28 or 58 days' interest depending on the remaining loan term. This is described in more detail in the _Your Loan Explained_ document, which is presented to the user along with their credit agreement [at the end of their application](https://docs.nwboxed.com/natwest-boxed-docs/v1.0.11/docs/white-label-unsecured-personal-loan-application-overview#7-credit-agreement-acceptance) and emailed to them afterwards.

<Callout icon="ℹ️" theme="info">
  Making an extra payment reduces the loan term. The monthly repayment amount is not reduced.
</Callout>

To make an extra payment:

1. The user selects either:
   1. The **Make extra payment** button on the loan dashboard
   2. The menu icon&#x20;


      <Image src="https://files.readme.io/c39652f2ab5770e8de15ea5d428ddeb5bf51188c18eed6275c758f09b08bbc0c-image.png" alt="menu icon" width="15px" />


      &#x20;in the top-left of the screen, and then selects **Make extra payment**


<Image src="https://files.readme.io/712fe6c5b6d490a977d3eb925855a914839fcf9fe59f04db8904291e384be315-image.png" align="center" width="200px" />


The user makes an extra payment by completing a transfer through their bank’s app or online banking platform. This screen provides step-by-step instructions to guide them through the process:

<Callout icon="📘" theme="info">
  The extra payment can be made from any of the user's bank accounts, not just the bank account the loan was originally paid into.
</Callout>

2. The user navigates to their online banking platform and starts a payment.
3. The user uses the account name, account number and sort code listed in the NatWest Boxed white label app as the payee.
4. The user completes the payment.

A successful extra payment will be listed on the [loan dashboard](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#the-loan-dashboard) as an _Additional payment_ with the outstanding balance and loan term adjusted accordingly. The fee is added to their outstanding loan balance.

### Request early settlement

A user can request to settle their loan before the end of the loan term. NatWest Boxed will generate an early settlement quote that includes additional fees and they’ll have to pay either 28 or 58 days interest (or the number of days remaining on their loan term if less) depending on the details of their credit agreement.

<Callout icon="🚧" theme="warn">
  Users cannot request an early settlement quote if they received their loan in the last 14 days. They should [submit a withdrawal request](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#withdraw-from-loan-agreement) instead.
</Callout>


<Image src="https://files.readme.io/caf5d260864c4d41a45e5fa77aa9538233746b805888caf21318facd8f82ddf2-UPL_request_settlement_Jan2026.png" align="center" width="420px" />


<br />

To request an early settlement quote:

1. The user selects the menu icon&#x20;


   <Image src="https://files.readme.io/c39652f2ab5770e8de15ea5d428ddeb5bf51188c18eed6275c758f09b08bbc0c-image.png" alt="menu icon" width="15px" />


   &#x20;in the top-left of the screen, and then selects **Request early settlement.**
2. The following screen provides additional information about the process. The user selects **Request early settlement quote**.
3. NatWest Boxed generates a quote that includes the total amount to settle the loan, based on:

* The outstanding balance of the loan
* Outstanding accrued interest
* The early repayment charge, defined in the credit agreement
* The total repayment pending

The quote is emailed to the user and is valid for 28 days. It's also available in this part of their account during that period if they try to request another quote.


<Image src="https://files.readme.io/3d3103478bddc976b741e694130ec48a8f076d5ede4e2571c13c0dcccc32c268-image.png" align="center" width="200px" />


<br />

4. To settle the loan, the user [makes an extra payment](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#make-an-extra-payment) for the amount defined in the early settlement quote.

### Withdraw from loan agreement

The user can withdraw from their loan agreement within 14 days after the credit agreement is sent to their email address.

They'll have 30 days from the date they contact NatWest Boxed to withdraw to repay the loan in full. They won’t have to pay any interest if they repay within the 30 day period.


<Image src="https://files.readme.io/f7ec88a274c818a4419cfb0e97dbbd2956e4aa499215091e07a7992af2fdeb63-UPL_withdraw.png" align="center" width="450px" />


<br />

To withdraw from their loan agreement:

1. The user selects the menu icon&#x20;


   <Image src="https://files.readme.io/c39652f2ab5770e8de15ea5d428ddeb5bf51188c18eed6275c758f09b08bbc0c-image.png" alt="menu icon" width="15px" />


   &#x20;in the top-left of the screen, then selects **Loan withdrawal**.
2. The user selects **Withdraw your loan**.
3. NatWest Boxed generates a quote that includes the total amount to settle the loan and emails this to the user. As this is an early withdrawal, the quote is the full balance of the loan with no interest or fees.
4. The user [makes an extra payment](https://docs.nwboxed.com/natwest-boxed-docs/docs/white-label-lending-user-journeys#make-an-extra-payment) for the amount defined in the quote to complete the withdrawal.

If the user doesn’t make the extra payment, the loan term will continue as normal.

### View annual statements

Account statements are generated annually on the date of the original loan disbursement and covers the previous 365 days. NatWest Boxed sends the user an email when a new annual statement is available.

Annual statements are regulatorily compliant and give a full summary of the past year’s activity on the loan, including: test

* Opening balance
* Closing balance
* Remaining loan term
* Repayments
* Interest accrued


<Image src="https://files.readme.io/52824f9e2357532fdc611623b4441820474c50296d0046174147c18aed8ddf47-image.png" align="center" width="200px" />


<br />

To view their statement:

1. The user selects the menu icon&#x20;


   <Image src="https://files.readme.io/c39652f2ab5770e8de15ea5d428ddeb5bf51188c18eed6275c758f09b08bbc0c-image.png" alt="menu icon" width="15px" />


   &#x20;in the top-left of the screen, then selects **Annual statements**.
2. The statements screen shows a list of all the available annual statements. The user selects the download icon&#x20;


   <Image src="https://files.readme.io/e8681c15b2a96eed2d905cf53d227c66e361ab086b4c49aedb1fc330243aab57-image.png" alt="download icon" width="15px" />


   &#x20;to view a specific statement.
3. The statement is downloaded to the user’s device as a PDF.

## Closed account

If the user logs into their account after paying off their loan or withdrawing from the agreement, the loan dashboard will reflect that. They will only be able to access their profile and contact NatWest Boxed’s support team in the hamburger menu.

![](https://files.readme.io/997836a3369b5f24601df3cd5a1989697815f68be9e8a371da9ee6bea15b88b4-image.png)

<br />

<br />
