---
title: Multi-Tenancy
excerpt: >-
  Manage client organizations with multi-user admin access and centralized
  billing.
deprecated: false
hidden: false
link:
  new_tab: true
  url: https://controld.com/features/multi-tenancy
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

Multi-Tenancy in the context of Organizations is a feature offered by Control D that enables businesses to effectively manage their DNS infrastructure across various units within the organization. It streamlines DNS management and offers the flexibility to cater to diverse operational requirements within a single umbrella organization.

# Problem Solved

Multi-Tenancy addresses the complexity of managing internet access and policies across different departments, subsidiaries, or customer accounts within a large enterprise or service provider setting. This feature allows businesses to:

* Manage end-user devices or network settings across the entire organization
* [Rapidly deploy](doc:provisioning) DNS settings to a large number of devices, utilizing tools like Remote Monitoring and Management (RMM)
* Provide team members with tailor-made access to view or modify DNS configurations
* Organize Profiles (policies) and Devices into Sub-Organizations for better control and delegation

# Feature Benefits

* **Centralized Management**: One-stop shop to manage the overall DNS policy and Profiles for various branches or units.
* **Customizable Access**: Grant selected permissions to team members to manage different aspects of the organization's assets.
* **Segmented Control**: Create Sub-Organizations representing different departments or customer groups, each with its custom settings.
* **Compliance and Security**: Option to lock down resolvers to pre-defined IP addresses, enhancing security and ensuring compliance with company policies.
* **Operational Efficiency**: Share Profiles between Sub-Organizations to maintain consistency and streamline the application of changes. Enforce [Global Profiles](doc:multiple-enforced-profiles) and avoid duplication. 
* **Enhanced Administration**: Update essential details, manage 2FA/MFA settings, and control data storage preferences from the My Organization tab.

# Implementing Multi-Tenancy

To leverage Multi-Tenancy within Organization accounts, businesses need to:

1. Navigate to the [My Organization](ref:organization) tab to manage company details and customization settings of main organization. 
2. Invite [team members](doc:org-members-permissions) with appropriate privileges into your main organization. 
3. Create and manage [Sub Organizations](doc:org-sub-organizations) to represent distinct units with their dedicated assets. Management and permissioning scheme is identical to the parent organization.
