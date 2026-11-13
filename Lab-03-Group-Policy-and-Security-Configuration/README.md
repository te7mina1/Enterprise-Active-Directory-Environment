# Lab-03-Group-Policy-and-Security-Configuration

Group Policy configuration and security-baseline experiments in the `allsafe.local` lab.

## Overview

This lab records selected Group Policy and security-baseline experiments on the Active Directory environment. The screenshots document policy configuration; they do not, by themselves, prove that the settings were applied to a client or that the resulting configuration is secure.

## Objectives

- Configure and review Group Policy settings for the intended domain or OU scope.
- Document Restricted Groups and local-administrator membership experiments.
- Review password-policy settings and a Microsoft Defender Antivirus policy experiment.
- Identify what still needs effective-policy verification and remediation.

## Lab Environment

| Component | Value |
|---|---|
| Domain | `allsafe.local` |
| Domain Controller | `AllSafeCS-DC01` — `192.168.56.10` |
| Client | `Domain-Client` — Windows 11 Pro 25H2 |
| Virtualization | Oracle VirtualBox |
| Tools | Group Policy Management, Group Policy Management Editor, Active Directory Users and Computers |

## Techniques and Tools

- Group Policy Management and Group Policy Management Editor
- Password policy and Restricted Groups configuration
- Group Policy Results / `gpresult` and Group Policy operational logs for planned validation

## Methodology

1. Reviewed password-policy settings shown in the Default Domain Policy, including a configured minimum password length of eight characters.
2. Reviewed the `Restricted Client Administrators` GPO and its Restricted Groups configuration.
3. Recorded the displayed `Client Admins` membership relationship and the local Administrators membership evidence.
4. Documented a separate policy with **Turn off Microsoft Defender Antivirus** set to **Enabled** as an intentionally unsafe lab experiment—not as a recommended baseline.
5. Marked effective-policy verification and restoration of the normal Defender posture as follow-up work.

## Findings

- The policy editor screenshot shows a minimum password length of eight characters. Confirm the intended value against the lab's security requirements.
- The Restricted Groups configuration shows `ALLSAFE\gideon.goddard` as a member of `Client Admins` and `Client Admins` as a member of `ALLSAFE\Domain Computers`. Verify that this relationship is intentional before applying or retaining it.
- The Defender policy screenshot shows **Turn off Microsoft Defender Antivirus: Enabled**. This is an unsafe setting for normal use and should be reverted after the controlled experiment.
- Available screenshots show configuration and membership views, not a Group Policy Results report proving what the client actually received. Application and remediation remain unverified.

## Methodology and verification still required

Run Group Policy Results or `gpresult` on the intended test client after policy refresh, inspect relevant Group Policy operational logs, confirm the GPO link and security filtering, and verify local group membership and Defender status. Record the results before marking the lab complete.

## Lessons Learned

- Scope each GPO deliberately and verify the targeted users and computers.
- A setting visible in the editor is not proof of effective application.
- Restricted Groups can enforce membership; validate the complete intended membership list before applying it.
- Disabling antivirus is not a security baseline. Restore and verify the normal protection state after experimentation.

## Conclusion

The configuration experiments are documented, but effective application, group-membership intent, and remediation have not yet been verified. Keep this lab in progress until those checks are captured.
