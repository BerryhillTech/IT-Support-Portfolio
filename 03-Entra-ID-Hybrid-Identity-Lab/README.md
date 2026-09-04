# Entra ID & Hybrid Identity Lab

## Overview

This project extends the Berryhill Technologies environment into Microsoft Entra ID, covering cloud identity provisioning, role-based access through security groups, Conditional Access-based MFA enforcement, and hybrid identity synchronization with the existing on-premises Active Directory domain.

## Lab Environment

- **Cloud Directory:** Microsoft Entra ID (Microsoft 365 tenant — dberryhillhotmail.onmicrosoft.com)
- **On-Premises Domain:** berryhill.local (Windows Server DC01, from the Active Directory Help Desk Home Lab)
- **Hypervisor:** VMware Workstation
- **Company:** Berryhill Technologies

## Objectives

- Provision cloud user identities with realistic organizational attributes
- Implement role-based access control using Entra ID security groups
- Enforce multi-factor authentication through a Conditional Access policy scoped to an elevated-access group
- Troubleshoot a real sign-in/authentication issue and document the resolution
- Establish hybrid identity by synchronizing the on-premises AD domain to Entra ID using Azure AD Connect

## User Provisioning

Two cloud identities were created to represent a standard employee and an IT staff member, consistent with the personas used in the Active Directory Help Desk Home Lab.

### Jordan Davis — Standard User

| Attribute | Value |
|---|---|
| Display Name | Jordan Davis |
| User Principal Name | jdavis@dberryhillhotmail.onmicrosoft.com |
| Job Title | Sales Associate |
| Department | Sales |
| Company Name | Berryhill Technologies |
| Usage Location | United States |

### Alex Johnson — IT Staff

| Attribute | Value |
|---|---|
| Display Name | Alex Johnson |
| User Principal Name | ajohnson@dberryhillhotmail.onmicrosoft.com |
| Job Title | IT Support Specialist |
| Department | IT |
| Company Name | Berryhill Technologies |
| Usage Location | United States |

Both accounts were created with an auto-generated temporary password and **"Require this user to change their password at next sign-in"** enabled, following standard account provisioning security practice.

### Evidence

![Jordan Davis User Creation](screenshots/01-jordan-davis-user-creation.png)

![Alex Johnson User Creation](screenshots/02-alex-johnson-user-creation.png)

## Security Group — Role-Based Access

An **IT-Support** security group was created to represent elevated IT access at the identity level, separate from the on-premises **IT-Staff** group used for file share permissions in the Active Directory lab. This reflects a realistic hybrid environment where cloud-native groups and on-premises-synced groups can coexist and serve different access-control purposes.

- **Group Name:** IT-Support
- **Group Type:** Security
- **Membership Type:** Assigned
- **Description:** Members with elevated IT support access to Berryhill Technologies cloud resources and applications
- **Members:** Alex Johnson

Jordan Davis was intentionally left out of this group to demonstrate that standard employees retain baseline access only.

### Evidence

![IT-Support Group Membership](screenshots/03-it-support-group-membership.png)

## Multifactor Authentication & Conditional Access

**Status:** Completed

### Objective
Move beyond baseline Security Defaults to a scoped, group-based Conditional
Access policy — enforcing MFA specifically for the IT-Support group rather
than tenant-wide, mirroring how a real organization layers identity
protection as it grows past a single trial tenant.

### Steps
1. Disabled Security Defaults (Entra ID → Properties → Manage security
   defaults), since Security Defaults and Conditional Access policies
   cannot both govern sign-in enforcement at the same time.
2. Created a new Conditional Access policy, **IT-Support - Require MFA**:
   - **Users/groups:** IT-Support (1 group)
   - **Target resources:** All cloud apps
   - **Grant control:** Require multifactor authentication
   - **Enable policy:** On
3. Verified the policy in the Conditional Access policy list, confirming
   state, scope, and grant control matched the intended configuration.

### Evidence

![Completed Conditional Access policy creation form](screenshots/conditional-access-policy-form.png)
*Completed policy creation form before saving — IT-Support group scoped, MFA grant control, policy enabled*

![Policy details confirming the deployed configuration](screenshots/conditional-access-policy-details.png)
*Policy details pane confirming State: On, 1 group scoped, MFA required*

### Verification
Policy details pane confirms: State On (recommended), 1 group included,
0 users/groups/roles excluded, All resources targeted, Require
multifactor authentication as the grant control.

## Sign-In Troubleshooting Scenario

*Status: Pending.*

## Hybrid Identity Sync — Azure AD Connect

*Status: Pending — will synchronize berryhill.local with this Entra ID tenant.*

## Tools and Technologies

- Microsoft Entra ID
- Microsoft 365 Admin Center
- Conditional Access
- Azure AD Connect *(pending)*

## Skills Demonstrated

- Cloud identity provisioning
- Role-based access control (RBAC) via security groups
- Organizational identity attribute management

*This list will expand as MFA, sign-in troubleshooting, and hybrid sync are completed.*

## Project Status

**In Progress**
