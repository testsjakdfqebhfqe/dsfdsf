---
title: Members and Permissions
excerpt: Invite team members to manage your organization and assign permission levels.
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: org-sub-organizations
      title: Sub Organizations
      type: basic
---
# What are Members

When you create your Organization, you become the owner and the sole member of the Organization. Chances are, you probably want to grant access to other folks on your team. Here's how you do it. 

# Adding Members

To add a new member to your organization, simply go to the [My Organization area](https://controld.com/dashboard/my-org), click the `Add Member` button and fill out the form.

<Image align="center" width="77% " src="https://files.readme.io/fee7b8a4ada6b936a9443ebe889ddcd4f69ac6b41d082fcaf1cdf4b6e1a0039e-Invite_Member.png" />

* **Email**: Email address of the person you wish to invite to your organization
* **Permission Level**: Desired permission level

Invited members can create their account with either a password or a [passkey](doc:passkeys) directly from the invite. They do not need to create a username/password account first before joining your Organization.

## Permission Levels

Currently, there are 3 permission levels to choose from:

* **Viewer**:
  * Allowed:
    * View all Profiles, Devices, and Analytics data.
  * Not Allowed:
    * Make changes to Profiles, Devices, or any other scopes.
    * Create, modify, or delete API tokens and Provisioning codes.

* **Admin**:
  * Allowed:
    * Create, modify, and delete Profiles, Devices, API tokens, and Provisioning codes.
    * Perform write actions within the organization.
  * Not Allowed:
    * Modify Organization membership.
    * Update Organization details.
    * Create new Sub-Organizations.

* **Owner**:
  * Allowed:
    * Full access to all actions within the Organization.
    * Modify Organization membership, update details, and create new Sub-Organizations.
    * Manage Profiles, Devices, API tokens, and Provisioning codes without restrictions.
    * Configure Single Sign-On (SSO) settings, including Okta OIDC integration.

# Single Sign-On Support

We now support Single Sign-On (SSO) using Okta OIDC and Microsoft EntraID OIDC. For details on how to configure and enable SSO for your organization, refer to our 

* [Okta Single Sign-On documentation](https://docs.controld.com/docs/okta-single-sign-on).
* [Microsoft EntraID Single Sign-On documentation](https://docs.controld.com/docs/sso-oidc-with-entraid) 

# Managing Members

Once you've added a second member to your Organization, you can change their permission level using the dropdown menu or eject them from the Organization. This will also delete their Control D account **and nullify any API tokens that they have created.** 

![](https://files.readme.io/3e1f58d2504a1dddfacf44d25100270cd09f1ab329d9c53a555597ff1d0bbf75-image.png)

All members of the parent Organization have the same permission level within all child Sub-Organizations.
