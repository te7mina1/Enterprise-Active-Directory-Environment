# Lab-02-Domain-Objects-and-Client-Integration

## Overview

This lab documents the creation and organization of sample Active Directory organizational units (OUs), users, and groups, followed by joining the Windows 11 client `Domain-Client` to `allsafe.local`. Evidence includes the initial domain-controller contact failure, the later successful join, domain-user sign-in, and the client computer object in Active Directory Users and Computers.

## Objectives

- Create and organize domain OUs, user accounts, and security groups.
- Join the Windows client to `allsafe.local`.
- Verify the successful join with a domain sign-in and the client computer object.
- Record troubleshooting evidence without including passwords or other secrets.

## Lab Environment

| Component | Value |
| --- | --- |
| Domain | `allsafe.local` |
| Domain Controller | `AllSafeCS-DC01` — `192.168.56.10` |
| Client | `Domain-Client` — Windows 11 Pro 25H2 |
| Client IP | `192.168.56.111` (recorded in the project README) |
| Virtualization | Oracle VirtualBox |
| Directory tools | Active Directory Users and Computers; Windows domain-membership settings |

## Techniques and Tools

- Active Directory Users and Computers for reviewing OUs, user accounts, groups, and computer objects
- Windows 11 system settings for domain membership and domain sign-in
- VirtualBox for the client VM

## Methodology

1. Created sample OUs, user accounts, and security groups in `allsafe.local` and reviewed their organization in Active Directory Users and Computers.
2. Configured the Windows 11 client, named `Domain-Client`, for membership in `allsafe.local`.
3. Recorded an initial attempt that reported the Domain Controller could not be contacted. The available evidence does not establish the cause, so no cause is assumed here.
4. Later evidence shows a successful domain join, a sign-in as `gideon.goddard@allsafe.local`, and the `DOMAIN-CLIENT` computer object in Active Directory Users and Computers.

## Findings

- The directory screenshots show OUs including `Accra`, `USA` (with `IT-Security-1` and `IT-Security-2`), `Dansoman`, and `AllSafe-Groups`. They show sample user accounts including Angela Moss and Gideon Goddard.
- The group screenshot shows `GG-AllSafe-Business`, `GG-AllSafe-Executives`, and `GG-AllSafe-IT-Security`. The description on `GG-AllSafe-Executives` says “Member of DA”; verify its actual membership and privilege intent before describing the configuration as least-privilege.
- A separate roadmap diagram presents a recommended OU/group layout. Treat it as a design reference, not proof that every item in that diagram was deployed exactly as shown.
- The initial client join attempt failed with a Domain Controller contact message; later screenshots show the `allsafe.local` welcome message and domain-user sign-in.
- A user-account screenshot shows `Password never expires` selected. Review that setting, and sanitize screenshots and rotate any lab credentials before publishing. No passwords are included in this README.

## Screenshots

Only images corresponding to domain objects, OU/group organization, Windows client domain joining, and domain sign-in are included below.

## Lessons Learned

- Keep user and computer objects in clearly scoped OUs, and use groups for role-based access where appropriate.
- A successful join should be verified on both sides: the client reports domain membership, and the computer object is visible in Active Directory.
- Preserve failed attempts as troubleshooting evidence, but distinguish them from the later verified result.
- Review privileged group membership and account password settings before calling the lab secure.

## Conclusion

The available evidence documents sample directory objects, a successful Windows client domain join, and a domain-user sign-in. The initial contact failure is retained as troubleshooting history. Review the indicated group membership and account settings, and sanitize the screenshots before any public release.
