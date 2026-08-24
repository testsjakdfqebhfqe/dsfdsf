---
title: Google Chrome Enterprise Deployment
excerpt: >-
  If you manage Chrome browsers or Chromebooks with Google Admin Console (Chrome
  Enterprise), you can enforce Control D DNS policies using DNS over HTTPS (DoH)
  with identifiers. This guide walks you through choosing an endpoint strategy,
  configuring Control D, and pushing settings to your users.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Overview

At a high level, you will:

1. Decide whether to use **one Endpoint for an entire OU** or **one Endpoint per User Group**.
2. **Create an Endpoint** in Control D and link it to the desired Profile (policy).
3. **Configure DNS over HTTPS with identifiers** in Google Admin Console using a template URL.
4. **Verify Clients** in the Control D dashboard once users sign in and start browsing.

***

## Plan your deployment

You have two main options for how to structure Endpoints in Control D.

### Option 1: Single Endpoint per Organizational Unit (OU)

Use this if:

* All users in a given OU should have the **same policy**.
* You want a **simpler setup** with fewer Endpoints to manage.

**Pros**

* Only one Endpoint to create and maintain.
* Simple mental model: 1 OU → 1 Endpoint.

**Cons**

* Harder to apply different policies to different user groups within that OU.
* Less granular reporting if users from many groups share the same Endpoint.

### Option 2: Separate Endpoint per User Group

Use this if:

* You want **different policies** for different user groups (e.g., Staff, Students, Guests).
* You want **cleaner Analytics** per group.

**Pros**

* Easy to see traffic and apply policies **per User Group**.
* More flexible if requirements change over time.

**Cons**

* You must repeat the setup **once per Group**.
* Slightly more effort to maintain.

> ### Recommendation
>
> If you need different policies for different sets of users, create **one Endpoint per User Group**. If everyone should share the same policy, a **single Endpoint per OU** is simpler.

***

## Step 1: Create an Endpoint in Control D

1. In the Control D dashboard, go to **Endpoints**.

2. Create a new Endpoint:

   * Give it a meaningful name (e.g., `Chrome - Staff`, `Chrome - Students`, or `Chrome - All Users`).
   * Link it to the **Profile** (policy) you want to enforce for that OU or Group.

3. Once the Endpoint is created, locate its **DoH resolver URL**. It will look like this:

   ```text
   https://dns.controld.com/YOUR_RESOLVER_ID
   ```

4. Copy this URL. You’ll need it for the Google Admin Console.

***

## Step 2: Configure DNS over HTTPS with identifiers in Google Admin Console

1. Go to the **Google Admin Console**.

2. Navigate to:

   **Devices → Settings → DNS over HTTPS with identifiers**
   (Exact path/label may vary slightly depending on your Admin Console version.)

3. In the **DNS-over-HTTPS templates with identifiers** box, enter:

   ```text
   https://dns.controld.com/YOUR_RESOLVER_ID/${USER_EMAIL}
   ```

   Replace `YOUR_RESOLVER_ID` with the ID from your Control D Endpoint URL.

4. (Recommended) If available in your Admin Console, set a value for the salt used for hashing identifiers in URI templates and keep it consistent long-term. If you leave this blank, Chrome will still hash identifiers, just without a salt.

5. Save your changes.

> ### Why `${USER_EMAIL}`?
>
> `${USER_EMAIL}` provides a per-user value that Chrome can use to generate a consistent identifier per signed-in user.
>
> **Important:** ChromeOS does **not** send `${USER_EMAIL}` to the DNS resolver in plain text. Instead, it hashes identifier values and sends the hash (hex-encoded) in the request URL.
>
> **What you should expect in Control D:** a Client will appear per user, but the Client name/identifier will be a **hashed string**, not the user’s email address. Because this is a one-way hash, Control D cannot automatically map it back to the email address.
>
> **About the salt:** If you set a salt, the hash changes based on that salt. If you later change the salt, the identifiers will change and you may see “new” Clients appear for the same users.

***

## Step 3: Rollout and expected behavior

After you save the policy:

1. The next time a managed **Chromebook user signs in**, the new DoH setting will be applied to their Chrome session.
2. As soon as they access the Internet:

   * Their device will start sending DNS queries to **Control D over HTTPS**.
   * A new **Client** will appear under the **Clients** list for the configured Endpoint in the **Analytics** section of the Control D dashboard.
3. Each Client entry will be associated with a **hashed identifier** derived from the configured variable (for example `${USER_EMAIL}`) and your optional salt, not the raw email address.

You can click on a Client in the Control D dashboard to:

* View that Client’s DNS activity.
* Confirm that the correct Profile is being enforced.
* Troubleshoot any access or filtering issues.

***

## Verifying the setup

To confirm everything is working:

1. Have a test user sign in to a managed Chromebook.
2. Browse to a few websites that should be **allowed** and a few that should be **blocked** based on your Profile.
3. In Control D, go to **Analytics → Clients**:

   * Look for a **new Client** under the correct Endpoint (it will typically look like a hash value, not an email).
   * Open it and confirm that their queries and blocks align with your configured rules.

If you don’t see the Client:

* Confirm the device is enrolled and receiving Chrome policies.
* Double-check the DoH template URL (resolver ID and `${USER_EMAIL}`).
* Verify that the Endpoint is linked to the correct Profile in Control D.

***

That’s it. Your Chrome Enterprise environment should now be using Control D via DNS over HTTPS, with per-user Client entries based on Chrome’s hashed identifiers.
