# Active Directory User Onboarding --- Sarah Johnson

<!---
![Platform](https://img.shields.io/badge/Platform-Windows%20Server-0078D4?style=for-the-badge&logo=windows)
![Directory](https://img.shields.io/badge/Directory-Active%20Directory-0A66C2?style=for-the-badge&logo=microsoft)
![Automation](https://img.shields.io/badge/Administration-PowerShell-5391FE?style=for-the-badge&logo=powershell)
![Virtualization](https://img.shields.io/badge/Virtualization-VirtualBox-183A61?style=for-the-badge&logo=virtualbox)
![Lab](https://img.shields.io/badge/Environment-Isolated%20Lab-555555?style=for-the-badge)
--->

## Overview

This lab documents an employee onboarding request in the `allsafe.local`
Active Directory environment. I created a domain user for Sarah Johnson,
placed the account in the Finance department OU, created and assigned
the `Finance-Security` security group, and verified the account by
signing in from the Windows 11 domain client.

The exercise demonstrates a basic service-desk-to-Active-Directory
workflow using both Active Directory Users and Computers (ADUC) and
PowerShell.

> **Lab note:** This is a simulated onboarding ticket in an isolated
> lab. Replace the ticket ID, requester, priority, and date placeholders
> below with the values recorded in your own ticketing exercise. Do not
> publish real employee credentials or sensitive production information.

## Ticket details

  ----------------------------------------------------------------------------------------
  Field                               Value
  ----------------------------------- ----------------------------------------------------
  Ticket ID                           `AS-ONB-001`

  Category                            Service Request --- User Provisioning

  Request                             Create a new employee domain account and grant
                                      Finance group membership

  Employee                            Sarah Johnson

  Department                          Finance

  Requested OU                        `OU=Finance-Department,OU=USA,DC=allsafe,DC=local`

  Account                             `sarah.johnson`

  User Principal Name                 `sarah.johnson@allsafe.local`

  Security group                      `Finance-Security`

  Priority                            Normal

  Status                              Completed

  Requester                           Not recorded

  Date                                13 November 2026
  ----------------------------------------------------------------------------------------

## Environment

  -----------------------------------------------------------------------
  Component                           Configuration
  ----------------------------------- -----------------------------------
  Active Directory domain             `allsafe.local`

  Domain controller                   `AllSafeCS-DC01`

  Domain controller IP                `192.168.56.10`

  Client                              Windows 11 VM (`Domain-Client11`)

  Hypervisor                          Oracle VirtualBox

  Administration tools                ADUC, Active Directory PowerShell
                                      module, Windows Command Prompt

  Network                             Isolated VirtualBox host-only lab
                                      network
  -----------------------------------------------------------------------

## Work performed

1.  I created the `Finance-Security` global security group in the
    Finance department OU.
2.  I created the Sarah Johnson user object in the `Finance-Department`
    OU.
3.  I assigned the logon name `sarah.johnson` and UserPrincipalName
    `sarah.johnson@allsafe.local`.
4.  I added Sarah Johnson to `Finance-Security`.
5.  I verified group membership in the group's **Members** tab and the
    user's **Member Of** tab.
6.  I queried the account with PowerShell and confirmed that it was
    enabled and a member of `Finance-Security`.
7.  I signed in to the Windows 11 domain client as Sarah and ran
    `whoami`.

## Verification

PowerShell account and membership check:

``` powershell
Get-ADUser sarah.johnson -Properties Department,MemberOf |
    Format-List Name,SamAccountName,Enabled,Department,MemberOf
```

The captured output confirmed:

-   `Name`: Sarah Johnson
-   `SamAccountName`: `sarah.johnson`
-   `Enabled`: `True`
-   `MemberOf`:
    `CN=Finance-Security,OU=Finance-Department,OU=USA,DC=allsafe,DC=local`

The `Department` attribute was blank in the captured output. The OU
placement does **not** automatically populate this attribute. If the
ticket requires it, set and verify it:

``` powershell
Set-ADUser sarah.johnson -Department "Finance"

Get-ADUser sarah.johnson -Properties Department |
    Select-Object Name,Department
```

The Windows client returned:

``` text
allsafe\sarah.johnson
```

This confirms the signed-in identity presented by the client. It does
not, by itself, prove that Finance application or file-share permissions
have been granted; those would require separate access tests and
authorization requirements.

## Security considerations

-   Use a unique, approved initial password and communicate it through
    an approved secure process. Never store passwords in this repository
    or report.
-   Require a password change at first logon where appropriate; the
    creation wizard indicated that this setting was selected.
-   Grant only the group memberships required for the employee's role.
-   Confirm the group is the correct security group and that its scope
    and membership align with the organization's access model.
-   Record the requester's authorization and retain evidence according
    to the organization's ticket-handling policy.
-   Avoid placing sensitive personal or operational information in
    account descriptions or public documentation.

## Outcome

The user object was created in the intended OU, added to the
`Finance-Security` group, and used to sign in to the Windows 11 domain
client. The PowerShell output confirmed the account was enabled and
listed the expected group membership.

**Follow-up:** Populate the AD `Department` attribute if it is required
by the ticket, and perform any resource-specific access test before
marking a real-world request fully closed.

## Evidence

Save the screenshots in this repository under `Lab-Shots/` using the
filenames below. The report includes the original screenshots supplied
for this exercise.

  Suggested filename                    Evidence
  ------------------------------------- ------------------------------------
  `01-user-creation.png`                New user creation confirmation
  `02-group-members.png`                Finance-Security group membership
  `03-select-user.png`                  User selection dialog
  `04-add-user-to-group.png`            Selected user for group membership
  `05-membership-confirmed.png`         Sarah listed in Finance-Security
  `06-powershell-ad-verification.png`   Get-ADUser verification
  `07-user-member-of.png`               User's Member Of tab
  `08-domain-sign-in.png`               Domain sign-in screen
  `09-whoami-domain-identity.png`       whoami result
  `10-windows-account-info.png`         Windows account information

## Skills demonstrated

-   Active Directory user provisioning
-   Organizational Unit placement
-   Global security group creation and membership management
-   ADUC administration
-   PowerShell account verification
-   Domain sign-in validation
-   Evidence collection and ticket documentation

<!---
## Suggested repository structure

``` text
AD-User-Onboarding/
├── README.md
├── report/
│   └── AD_User_Onboarding_Ticket_Report.docx
└── evidence/
    ├── 01-user-creation.png
    ├── 02-group-members.png
    ├── 03-select-user.png
    ├── 04-add-user-to-group.png
    ├── 05-membership-confirmed.png
    ├── 06-powershell-ad-verification.png
    ├── 07-user-member-of.png
    ├── 08-domain-sign-in.png
    ├── 09-whoami-domain-identity.png
    └── 10-windows-account-info.png
```
--->
