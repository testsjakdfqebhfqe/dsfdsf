---
title: 'SSO: OIDC with Okta'
excerpt: >-
  This guide walks you through the steps to configure Single Sign-on using OIDC
  with Okta.
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

Before you begin, ensure you have admin access to your Okta dashboard.

***

## Step 1: Set Up an Okta Application for Control D

**Note**: If you intend to use specific `controld-*` groups (e.g., `controld-admin`, `controld-owner`, `controld-viewer`) for role-based access, create these groups first as outlined in Step 4.

1. Log in to your [Okta Admin Dashboard](https://login.okta.com/).

2. Navigate to **Applications** and click **Create App Integration**.

3. Select **OIDC - OpenID Connect** as the sign-in method and choose **Web Application** as the application type. Click **Next**.

4. Fill in the application details:

   | Field                  | Data                                                                                                     |
   | :--------------------- | :------------------------------------------------------------------------------------------------------- |
   | App Integration Name   | Control D                                                                                                |
   | Logo (Optional)        | ![](https://files.readme.io/a676ae50d2677033218a97032bea07910ed1b37ce91da7bc915f05a70d96cf7f-cd_120.png) |
   | Sign-in redirect URIs  | `https://controld.com/sso/callback?provider=okta`                                                        |
   | Sign-out redirect URIs | Delete all entries                                                                                       |

   <br />

   > 📘 For IDP Initiated Login support
   >
   > This allows for one-click login from the Okta user homepage

   | Field                  | Data                                               |
   | :--------------------- | :------------------------------------------------- |
   | Login initiated by     | Either Okta or App                                 |
   | Application visibility | Display application icon to users                  |
   | Login flow             | Redirect to app to initiate login (OIDC Compliant) |
   | Initiate login URI     | `https://api.controld.com/okta/auth_init`          |

   <br />

   <Image align="center" src="https://files.readme.io/17815bf0b941d1a2fca4f8f83da0f8639ac1380e0544f2a494b772e51645e3c3-Screenshot_2025-02-17_at_8.50.28_PM.png" />

<br />

5. Under **Assignments**, you can assign people or groups to the application, or select **Skip group assignment for now** if you wish to assign them later.\
   If you plan to use role-based groups, assign the `controld-*` groups (`controld-admin`, `controld-owner`, `controld-viewer`) created earlier.

> 📘 `ControlD.*`and `controld-*` are both supported group formats.

6. Ensure the **Grant Type** is set to **Authorization Code**.
7. Click **Save** to create the application.

<Image align="center" width="600px" src="https://files.readme.io/62167edf3ba87c62fe4cf87bc0eeb790436f4e5049b722d36523c2e632ffb36c-Screenshot_2024-12-03_at_9.43.29_PM.png" />

***

## Step 2: Configure the Okta Application for Control D

1. Open the newly created Control D application in Okta.

2. Go to the **General Settings** tab and note down the **Client ID** and **Client Secret**.

3. Go to the **Sign On** tab and ensure the **OpenID Connect ID Token** option is enabled.

4. Under **Groups Claim**, set **Groups claim type** to **Filter** and choose **Starts With**. Enter `controld` to include groups such as `controld-admin`, `controld-owner`, and `controld-viewer`.

<Image align="center" width="600px" src="https://files.readme.io/e2abc6532ce666c961f4143fd5aa559a29f06709550c416043d0657d7111ba58-Screenshot_2024-12-03_at_9.51.42_PM.png" />

***

## Step 3: Assign User Groups in Okta

> 🚧 A feature to support custom group mappings is under way!

**Note**: If you have already created the `controld-*` groups, you can skip creating new groups and proceed to assign users to the appropriate permissions.

1. Go to **Directory > Groups** in Okta.

2. Create three groups for Control D access (if not already created):

   * `controld-admin`
   * `controld-owner`
   * `controld-viewer`

3. Assign users to these groups based on their roles and responsibilities within Control D.

> ❗️ Learn about the different roles and permission levels here: [https://docs.controld.com/docs/org-members-permissions#permission-levels](https://docs.controld.com/docs/org-members-permissions#permission-levels)

***

## Step 4: Add SSO Configuration in Control D

1. Log in to the Control D.

2. Navigate to **My Organization**, scroll to **SSO Provider**, and click the toggle to enable.

3. Fill in the required fields:

   * **Okta Domain:** `<your-subdomain>.okta.com`
   * **Client ID:** The value you copied from the Okta application.
   * **Client Secret:** The value you copied from the Okta application.
   * **Email Domains:** Enter the domains associated with your organization, e.g., `example.com`. This is necessary to map email domains to your Control D customer account so that login attempts are redirected to the correct Okta authentication server.

4. Click **Save** to enable Okta SSO for your organization.

<Image align="center" className="border" border={true} src="https://files.readme.io/1e7503248ac44ec14dd7ed3c525c618c63e9597dda1b7833c08fed6974d9a126-image.png" />

***

## Step 5: Test SSO Login

1. Log out of Control D and navigate to the login page.
2. Enter your Okta email address, leaving the password blank.
3. Click the **Log in with Okta** button.
4. Enter your Okta credentials and confirm successful login.
5. Verify role-based access permissions by testing users in the `controld-admin`, `controld-owner`, and `controld-viewer` groups.

***

## Troubleshooting

If you encounter any issues:

1. Verify the **redirect URIs** in your Okta application settings.
2. Ensure the user groups are correctly assigned in Okta.
3. Check the SSO configuration in the Control D Admin Panel for typos or missing fields.
4. Refer to the Okta logs for debugging SSO errors.

***

For additional support, contact [Control D Support](https://controld.com/contact).
