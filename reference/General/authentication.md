---
title: Authentication
excerpt: How to create and invalidate API tokens.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Generating API Tokens

<Image title="CD_-_The_Default_Rule_blog_header_v1.png" alt={1920} align="center" width="100%" src="https://files.readme.io/acb09f3-CD_-_The_Default_Rule_blog_header_v1.png" />

Head over to [API Tokens](https://controld.com/dashboard/api) section, and click on "+", give it a name, choose permission level and press Add.  

Tokens can have one of 2 permission levels:

* **Read** - Allows you to perform reads against the API, but won't let you change anything.
* **Write** - Full access token. Allows reads and writes. 

Optionally, you can set Allowed IPs when creating the token to restrict where it can be used from.

![](https://files.readme.io/0f6217b13429f7b4b9ad82eb39da461bbff2bc458e540e6fe2304e822f6ee6c6-image.png)

## Editing an existing token (type and allowed IPs)

You can update a token’s scope and network restrictions at any time:

1. In **API Tokens**, click pencil icon next to the token.
2. Change the **Type** (Read/Write) and/or **Allowed IPs** (comma-separated IPv4/IPv6 or CIDR).
3. Save your changes.

## Using API tokens

Supply your API token in the `Authorization` header as a Bearer token for all authenticated API calls.

**Example (cURL)**

```bash
curl https://api.controld.com/users \
  --header 'authorization: Bearer YOUR_FANCY_TOKEN'
```

If successful, you’ll see your account details.

## Invalidating API Tokens

Click the delete button next to the token name you wish to delete. 

## Using API Tokens

Supply your API token in the `Authorization` header, as a Bearer token in all authenticated API calls. 

```curl
curl https://api.controld.com/users --header 'authorization: Bearer YOUR_FANCY_TOKEN'
```

You should see your account details if you've done this correctly.
