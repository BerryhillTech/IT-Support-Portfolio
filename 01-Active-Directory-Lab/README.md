# Active Directory Help Desk Home Lab

## Project Overview

This project demonstrates the deployment and administration of a small Windows domain environment designed to simulate common IT Help Desk and Systems Administration responsibilities.

The lab was built using virtual machines and includes a Windows Server domain controller and a Windows 11 client workstation. The environment was used to practice Active Directory administration, DNS configuration, domain authentication, user and group management, password administration, SMB file sharing, NTFS permissions, and troubleshooting.

---

## Lab Environment

| System | Role |
|---|---|
| DC01 | Windows Server / Domain Controller |
| CLIENT01 | Windows 11 Domain-Joined Workstation |
| berryhill.local | Active Directory Domain |
| Active Directory Domain Services | Identity and authentication |
| DNS | Domain name resolution |
| PowerShell | Administration and troubleshooting |

---

## Active Directory Structure

I created an organizational structure representing a small business environment.

**Domain:** `berryhill.local`

**Organization:** `Berryhill Technologies`

Organizational Units (OUs) included:

- Computers
- Employees
  - Finance
  - HR
  - IT
  - Sales
- Groups

This structure allows users, computers, and security groups to be organized based on business function.

---

## User and Group Administration

Created test employee accounts to validate different permission levels within the domain.

**User:** Jordan Davis  
**Username:** `jdavis`

Jordan Davis was configured as a standard domain user and placed in the IT organizational unit. The account was used to represent a typical employee requiring read-only access to departmental resources.

**User:** Alex Johnson  
**Username:** `ajohnson`

Alex Johnson was used to represent an IT employee requiring elevated access to departmental resources.

I also created the following security group:

**Security Group:** `IT-Staff`

Alex Johnson was added to the `IT-Staff` security group, while Jordan Davis remained a standard domain user.

This configuration allowed access to resources to be controlled through security group membership rather than assigning permissions directly to individual users, demonstrating group-based access control.

---

## Domain-Joined Workstation

Configured a Windows 11 workstation named:

`CLIENT01`

The workstation was joined to:

`berryhill.local`

After joining the domain, I verified domain authentication by signing into CLIENT01 using domain accounts.

PowerShell was used to verify the workstation's domain membership and authenticated user context.

Example validation commands:

`hostname`

`whoami`

`(Get-CimInstance Win32_ComputerSystem) | Select-Object Name,Domain,PartOfDomain`

---

## DNS Configuration and Validation

CLIENT01 was configured to use the domain controller as its DNS server.

This allowed the workstation to locate Active Directory services and the domain controller.

DNS and Active Directory service discovery were validated using tools such as:

`ipconfig`

`nslookup berryhill.local`

`nslookup -type=SRV _ldap._tcp.dc._msdcs.berryhill.local`

The SRV lookup successfully identified `dc01.berryhill.local` as an LDAP service provider for the domain.

---

## SMB File Share and Permissions

Created a shared folder on DC01:

`C:\IT-Share`

The folder was published as an SMB network share:

`\\DC01\IT-Share`

Access was configured using group-based permissions rather than assigning permissions directly to individual users.

The final access model was:

- `Domain Users` — Read-only access
- `IT-Staff` — Modify access
- `Administrators` — Full Control
- `SYSTEM` — Full Control

Both SMB share permissions and NTFS permissions were reviewed to ensure the effective permissions matched the intended access model.

Jordan Davis was used to validate standard read-only access, while Alex Johnson was used to validate the additional permissions granted through membership in the `IT-Staff` security group.

This demonstrated the interaction between:

- Active Directory security groups
- SMB share permissions
- NTFS file system permissions
- Domain authentication
- Effective permissions

---

## Troubleshooting Scenario

During testing, access to the shared resource did not initially behave as intended.

Troubleshooting included:

- Verifying TCP 445 connectivity
- Confirming SMB share configuration
- Reviewing share permissions
- Reviewing NTFS permissions
- Verifying Active Directory group membership
- Refreshing Group Policy
- Checking the user's authentication token
- Reviewing Effective Access
- Testing access from CLIENT01

Commands used during troubleshooting included:

`Test-NetConnection DC01 -Port 445`

`net use`

`whoami /groups`

`gpupdate /force`

`Get-ADGroupMember "IT-Staff"`

`Get-SmbShareAccess -Name "IT-Share"`

The permissions were corrected so that standard domain users received read-only access while members of `IT-Staff` received modify access.

Client-side testing and Effective Access verification were then used to confirm that the permissions functioned as intended.

---

## Final Validation

The completed configuration was tested from CLIENT01 using domain user accounts with different permission levels.

The following were successfully verified:

- CLIENT01 was joined to `berryhill.local`
- Domain users could authenticate successfully
- CLIENT01 could communicate with DC01
- DNS successfully located Active Directory services
- Domain users could access `\\DC01\IT-Share`
- Jordan Davis had read-only access to the shared resource
- Jordan Davis could open files but could not save changes to protected files
- Alex Johnson was recognized as a member of `IT-Staff`
- Alex Johnson could modify content within the shared resource
- Group-based access control functioned as intended

Effective Access testing confirmed that Jordan Davis had read permissions without write, delete, or full-control permissions. A client-side test also confirmed that Windows denied a save attempt while authenticated as Jordan Davis.

Testing with Alex Johnson confirmed that membership in the `IT-Staff` security group provided the intended modify access.

---

## Skills Demonstrated

- Windows Server Administration
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- Organizational Unit Management
- User Account Administration
- Security Group Administration
- Group-Based Access Control
- Windows 11 Domain Joining
- DNS Configuration
- Active Directory DNS/SRV Records
- SMB File Sharing
- NTFS Permissions
- Effective Access Analysis
- PowerShell
- TCP/IP Troubleshooting
- Group Policy Refresh
- Authentication Troubleshooting
- Permissions Troubleshooting
- Technical Documentation

---

## Key Takeaways

This lab provided hands-on experience administering a Windows domain rather than working only with theoretical Active Directory concepts.

I practiced workflows an IT support professional may encounter when provisioning users, assigning group-based permissions, joining a workstation to a domain, configuring access to organizational resources, and troubleshooting authentication and permissions-related incidents.

The troubleshooting portion was particularly useful because it required validating multiple layers of the environment—including network connectivity, authentication, Active Directory group membership, SMB permissions, NTFS permissions, and Effective Access—to isolate and resolve issues.

The final configuration also demonstrated how security groups can be used to provide different levels of access based on a user's role rather than assigning permissions individually.

---

## Project Screenshots

The following screenshots provide validation of the completed Active Directory lab environment and key administrative tasks.

### 1. Active Directory Organizational Structure

The Active Directory environment was organized into departmental Organizational Units (OUs) representing a small business structure.

![Active Directory OU Structure](screenshots/01-active-directory-ou-structure.png)

### 2. Security Group and User Membership

The `IT-Staff` security group was configured to provide elevated departmental access through group membership, demonstrating role-based administration of resource permissions.

![IT-Staff Group Membership](screenshots/02-it-staff-group-membership.png)

### 3. Domain Authentication and File Share Validation

CLIENT01 was successfully joined to the `berryhill.local` domain, and domain authentication and access to the shared network resource were successfully validated.

![Domain and File Share Validation](screenshots/03-domain-share-validation.png)

### 4. DNS and Active Directory Service Discovery

DNS resolution and Active Directory service discovery were validated from CLIENT01. The LDAP SRV record successfully identified `dc01.berryhill.local` as the domain service provider.

![DNS and SRV Validation](screenshots/04-dns-srv-validation.png)
