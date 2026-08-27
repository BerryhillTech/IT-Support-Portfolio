# Help Desk Troubleshooting Lab

## Overview

This project simulates real-world Help Desk support incidents in a Windows domain environment. Each ticket documents the reported issue, troubleshooting process, root cause, resolution, and verification steps.

## Lab Environment

- **Hypervisor:** VMware Workstation
- **Domain Controller:** DC01 — Windows Server
- **Client Workstation:** Client01 — Windows 11
- **Directory Services:** Active Directory Domain Services (AD DS)
- **Test User:** Jordan Davis (jdavis)

## Objectives

- Troubleshoot common end-user IT support incidents
- Apply a structured troubleshooting methodology
- Perform Active Directory user account support
- Diagnose Windows workstation and access issues
- Document troubleshooting steps, root causes, and resolutions
- Practice Help Desk ticket documentation and escalation

## Ticket Documentation Format

Each simulated support ticket will include:

- **Ticket ID**
- **User / Workstation**
- **Issue Reported**
- **Priority**
- **Troubleshooting Steps**
- **Root Cause**
- **Resolution**
- **Verification**
- **Ticket Status**

## Support Tickets

| Ticket | Issue | Category | Status |
|---|---|---|---|
| HD-001 | Domain user unable to sign in | Account / Authentication | Resolved |
| HD-002 | Domain account locked after failed sign-in attempts | Account / Authentication | Resolved |
| HD-003 | User cannot access shared folder | Access / Permissions | Planned |
| HD-004 | Mapped network drive unavailable | File Services | Planned |
| HD-005 | User requires departmental resource access | Service Request | Planned |
| HD-006 | Windows application or user profile issue | Application / Windows | Planned |

### HD-001 — Domain User Unable to Sign In

**User:** Jordan Davis (`jdavis`)  
**Workstation:** Client01  
**Category:** Account / Authentication  
**Priority:** P3 — Normal  
**Status:** Resolved

#### Issue Reported

The user reported being unable to sign in to the Windows workstation because the existing password was being rejected.

#### Troubleshooting Steps

1. Reproduced the authentication issue on Client01.
2. Opened Active Directory Users and Computers (ADUC) on DC01.
3. Located the `jdavis` domain account and reviewed the account properties.
4. Verified that the account was not locked out and did not show an account expiration issue.
5. Determined that a password reset was the appropriate next troubleshooting action.
6. Reset the user's domain password through Active Directory.
7. Returned to Client01 and successfully authenticated with the updated credentials.
8. Ran `whoami` to verify the authenticated domain identity.

#### Root Cause

The user was unable to provide valid credentials for the domain account, resulting in failed authentication attempts on Client01.

#### Resolution

Reset the `jdavis` domain account password through Active Directory Users and Computers and restored the user's access to Client01.

#### Verification

After successfully signing in, the following command was executed on Client01:

`whoami`

The command returned:

`berryhill\jdavis`

This confirmed that Jordan Davis successfully authenticated using the domain account.

#### Evidence

![HD-001 Authentication Verification](screenshots/hd-001-authentication-verification.png)

### HD-002 — Domain Account Lockout

**User:** Jordan Davis (`jdavis`)  
**Workstation:** Client01  
**Category:** Account / Authentication  
**Priority:** P3 — Normal  
**Status:** Resolved

#### Issue Reported

The user reported being unable to sign in to Client01 despite attempting to use the correct password. Windows reported that the account was currently locked out.

#### Troubleshooting Steps

1. Reproduced the sign-in issue on Client01 and observed the Windows account lockout message.
2. Opened Active Directory Users and Computers (ADUC) on DC01.
3. Located the `jdavis` domain account and opened the account properties.
4. Verified that Active Directory reported the account as currently locked out.
5. Determined that a password reset was unnecessary because the issue was an account lockout rather than an invalid or forgotten password.
6. Used the **Unlock account** option in ADUC to restore account access.
7. Returned to Client01 and successfully authenticated using the user's existing credentials.
8. Ran `whoami` to verify the authenticated domain identity.

#### Root Cause

The domain account reached the configured account lockout threshold after multiple invalid authentication attempts.

#### Resolution

Unlocked the `jdavis` domain account through Active Directory Users and Computers without resetting the user's password.

#### Verification

After the account was unlocked, the user successfully signed in to Client01 using the existing credentials.

The following command was executed:

`whoami`

The command returned:

`berryhill\jdavis`

This confirmed that domain authentication was successfully restored.

#### Evidence

**Client-side lockout message:**

![HD-002 Client Lockout Message](screenshots/hd-002-client-lockout-message.png)

**Active Directory lockout confirmation:**

![HD-002 ADUC Locked Account](screenshots/hd-002-aduc-locked-account.png)

**Successful authentication after account unlock:**

![HD-002 Unlock Verification](screenshots/hd-002-unlock-verification.png)

## Troubleshooting Methodology

For each support incident, I will follow a structured troubleshooting process:

1. Identify and document the user's reported problem
2. Gather information and establish the scope of the issue
3. Develop and test a probable cause
4. Implement an appropriate solution
5. Verify full system functionality
6. Document the root cause, resolution, and verification
7. Escalate the issue when it exceeds the appropriate support scope

## Tools and Technologies

- Windows 11
- Windows Server
- Active Directory Users and Computers (ADUC)
- PowerShell
- Command Prompt
- VMware Workstation
- SMB file sharing
- NTFS permissions
- Windows administrative tools

## Skills Demonstrated

- Help Desk troubleshooting
- Incident management
- Service request fulfillment
- Active Directory account administration
- Windows workstation support
- Access and permissions troubleshooting
- Technical documentation
- Root cause analysis
- Ticket prioritization
- Issue escalation
- End-user support

## Project Status

**In Progress**
