# Identity & Access Management and IT Support Portfolio

I'm DeAirrius Berryhill, an IT support professional working toward Identity and Access Management. This repo documents the labs I've built to practice real identity and help desk work: provisioning users, managing access, enforcing MFA, troubleshooting sign-ins and syncing on-prem Active Directory with Microsoft Entra ID.

Every project is documented the way a help desk ticket would be: the environment, what I did, what broke, how I found the cause and how I verified the fix.

## Technical Focus

- Microsoft Entra ID & Hybrid Identity
- Active Directory Domain Services
- Access Management & Role-Based Access
- Conditional Access & Multifactor Authentication (MFA)
- Group Policy
- Windows 10/11 & Windows Server Administration
- Help Desk Troubleshooting & Ticket Documentation
- DNS & TCP/IP Fundamentals

## Projects

### 1. Active Directory Help Desk Lab
**Status:** Completed

Built a virtualized Windows domain in VMware with a Windows Server domain controller and a domain-joined Windows 11 client to practice everyday IT support and systems administration tasks.

**Skills:**
- Active Directory Domain Services
- User & Group Management
- Organizational Units
- Password Resets & Account Unlocks
- Domain-Joined Workstations
- Group Policy
- DNS
- File & Folder Permissions
- Help Desk Troubleshooting

[View Project](./01-Active-Directory-Lab/)

---

### 2. Help Desk Troubleshooting Lab
**Status:** Completed

Worked through six simulated support tickets covering locked accounts, permissions, mapped drives, group access and user profile issues. Each ticket is documented from the reported issue to root cause, resolution and verification.

**Skills:**
- Structured Troubleshooting Methodology
- Active Directory Account Support
- Access & Permissions Troubleshooting
- Service Request Fulfillment
- Root Cause Analysis
- Help Desk Ticket Documentation

[View Project](./02-Help-Desk-Troubleshooting-Lab/)

---

### 3. Entra ID & Hybrid Identity Lab
**Status:** Completed

Extended the Berryhill Technologies Active Directory lab into Microsoft Entra ID. Covers cloud identity administration, role-based access, Conditional Access, MFA, sign-in troubleshooting and hybrid sync between on-prem Active Directory and Entra ID.

**Skills:**
- Microsoft Entra ID Administration
- Cloud User Provisioning & Identity Management
- Role-Based Access Control (Security Groups)
- Conditional Access Policy Configuration
- Multifactor Authentication (MFA)
- Entra ID Sign-In Log Analysis
- Authentication & Credential Troubleshooting
- Administrative Password Reset & Account Recovery
- Microsoft Entra Connect Sync
- Password Hash Synchronization (PHS)
- Organizational Unit (OU) Sync Filtering
- Synchronization Engine & Metaverse Verification

**Key Implementations:**
- Provisioned cloud identities for standard and IT support users
- Created an IT-Support security group for role-based access
- Built a group-scoped Conditional Access policy requiring MFA
- Diagnosed a failed Microsoft 365 sign-in using Entra ID sign-in logs and error code `50126`
- Fixed the issue with an administrative password reset and confirmed access was restored
- Set up Microsoft Authenticator registration and verified MFA sign-in
- Configured Microsoft Entra Connect with Password Hash Synchronization
- Limited sync scope to a pilot Organizational Unit
- Verified identities through the sync engine and metaverse, then exported them to Entra ID
- Confirmed hybrid sign-in using synchronized on-prem credentials

[View Project](./03-Entra-ID-Hybrid-Identity-Lab/)

---

## Coming Next

| Lab | Focus |
|---|---|
| Intune & Endpoint Management | Device enrollment, compliance policies and configuration profiles, building on the Entra ID lab |
| PowerShell for IT Support | Scripting common account and Windows admin tasks |
| Network Troubleshooting | TCP/IP, DNS, DHCP and connectivity issues using Windows tools |
| Windows Endpoint Support | Event Viewer, Device Manager, Services and other admin tools |

## Tools & Technologies

`Microsoft Entra ID` `Microsoft Entra Connect` `Active Directory` `Group Policy` `Microsoft 365` `Windows Server` `Windows 11` `VMware Workstation` `DNS`

**Planned:** `Microsoft Intune` `PowerShell`

## Certifications & Training

- Microsoft Certified: Security, Compliance, and Identity Fundamentals (SC-900)
- CompTIA Security+ (SY0-701)
- Google IT Support Professional Certificate
- Google Cybersecurity Professional Certificate

## Connect

[LinkedIn](https://www.linkedin.com/in/deairriusberryhill)
