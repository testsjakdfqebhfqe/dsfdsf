---
title: 'SSO: OIDC with EntraID'
excerpt: >-
  This guide walks you through the steps to configure Single Sign-on using OIDC
  with Microsoft EntraID.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Prerequisites

Before you begin, ensure you have admin access to your EntraID dashboard.

***

## Step 1: Set Up an Application for Control D

<br />

1. Log in to your [Azure Portal](https://portal.azure.com/).

2. Navigate to **App registrations** and click **New Registration**.

3. Fill in the application details:

   | Field                 | Data                                                                                                     |
   | :-------------------- | :------------------------------------------------------------------------------------------------------- |
   | App Integration Name  | Control D                                                                                                |
   | Logo (Optional)       | ![](https://files.readme.io/a676ae50d2677033218a97032bea07910ed1b37ce91da7bc915f05a70d96cf7f-cd_120.png) |
   | Redirect URI          | `https://controld.com/sso/callback?provider=microsoft`                                                   |
   | Redirect URI Platform | Web                                                                                                      |

   <br />

***

## Step 2: Configure client credentials

1. Open the newly created Control D application in App Registrations.

2. Go to the **Certificates & secrets** tab then to **Client Secrets** and click **New Client Secret**.

3. Add the name **Control D** and click **Add**

4. Copy the new secrets **Value** property and store securely, you will need it in later steps.

<Image align="center" src="https://files.readme.io/0002338a918782c266d983c4587758a34adfb8506b5ce830767fe674dff4997f-Screenshot_2025-08-18_at_7.17.53_PM.png" />

***

<br />

## Step 3: Collect Application details

1. Navigate to the Control D application overview page. **App registrations**, then **Control D**

2. Note the **Application (client) ID** and **Directory (tenant) ID** values.

<Image align="center" src="https://files.readme.io/bb66859b8b126b7d8d2652f0c38ac28919c39fd963a64eb9d3daf380463f2e36-Screenshot_2025-08-18_at_7.17.09_PM.png" />

***

## Step 4: Create and Assign User Groups

> 🚧 A feature to support custom group mappings is under way!

1. Go to **Groups > New Group** from your Microsoft portal home screen.

2. Create three groups for Control D access:

   * `controld-admin` or `ControlD.Admin`
   * `controld-owner` or `ControlD.Owner`
   * `controld-viewer` or `ControlD.Viewer`

3. Assign users to these groups based on their roles and responsibilities within Control D.

<Image align="center" src="https://files.readme.io/66b584ea1f80b108ee82a07947eecf5ace9b3dec75254c98c0ac5d72fb3d38e8-Screenshot_2025-08-18_at_7.27.58_PM.png" />

> ❗️ Learn about the different roles and permission levels here: [https://docs.controld.com/docs/org-members-permissions#permission-levels](https://docs.controld.com/docs/org-members-permissions#permission-levels)

***

<br />

## Step 5: Set Application Group Claim

1. Navigate to **App registrations**, select **Control D** then **API Permissions**
2. Click **Add Permission**
3. Select **Microsoft Graph** then **Delegated Permissions**
4. Search for **Group**
5. Select **Group.Read.All** then click **Add Permission**
6. You will now need to grant admin consent by selecting the new **Group.Read.All** permission from the list, then click **Grant Admin Consent** next to the **Add Permission** button.
7. Click to **Yes** in the dialog popup to confirm Admin consent

<Image align="center" src="https://files.readme.io/d67d1b91a133ec42cb626e9775e33a33ed60edaf41ab74a362843121f33bc1d8-Screenshot_2025-08-20_at_7.48.48_PM.png" />

***

## Step 6: Add SSO Configuration in Control D

1. Log in to the Control D.

2. Navigate to **My Organization**, scroll to **SSO Provider**, and select **Microsoft**.

3. Fill in the required fields:

   * **Microsoft Tenant ID:** The value from previous steps
   * **Client ID:** The value you copied from the application.
   * **Client Secret:** The value you copied from the application client secrets tab.
   * **Email Domains:** Enter the domains associated with your organization, e.g., `example.com`. This is necessary to map email domains to your Control D customer account so that login attempts are redirected to the correct Microsoft tenant authentication server.

4. Click **Save** to enable EntraID SSO for your organization.

<Image align="center" src="https://files.readme.io/9942727ce5928ea379ef24b3f94f9a920dfeb47e430830425a91492d6f2fcab6-Screenshot_2025-08-18_at_9.05.10_PM.png" />

***

## Step 7: Test SSO Login

1. Log out of Control D and navigate to the login page.
2. Enter your Microsoft Organizations email address, leaving the password blank.
3. Click the **Log in with SSO** button.
4. You will be prompted to login to your Microsoft account.
5. Verify role-based access permissions by testing users in the `controld-admin`, `controld-owner`, and `controld-viewer` groups.

***

## Troubleshooting

If you encounter any issues:

1. Verify the **Redirect URI** in your App Registration settings.
2. Ensure the user groups are correctly assigned in the Microsoft panel.
3. Check the SSO configuration in the Control D Admin Panel for typos or missing fields.
4. Refer to the Microsoft logs for debugging SSO errors.

***

For additional support, contact [Control D Support](https://controld.com/contact).
