# Lab-01-Windows-Server-and-AD-DS-Deployment

Windows Server setup, AD DS installation, domain promotion, and DNS verification.

## Overview

This lab documents the evidenced deployment of a Windows Server domain controller for the `allsafe.local` lab domain. Scope is limited to initial Windows Server configuration, AD DS/DNS installation, promotion to a Domain Controller, and DNS checks. Later client, Group Policy, monitoring, and security-exercise work is outside this lab's completion claims.

## Objectives

- Configure the Windows Server VM, hostname, time zone, static host-only IP, and Remote Desktop.
- Install the Active Directory Domain Services (AD DS) and DNS roles.
- Promote the server to a Domain Controller and create the `allsafe.local` domain/forest.
- Verify forward DNS resolution for the domain and Domain Controller.

## Lab Environment

| Component | Value |
| --- | --- |
| Virtualization | Oracle VirtualBox |
| Server | `AllSafeCS-DC01` |
| Operating system | Windows Server 2025 Datacenter Evaluation |
| Domain | `allsafe.local` |
| Domain Controller IP | `192.168.56.10/24` on the host-only interface |
| VM resources | 4 GB RAM, 3 vCPUs, 70 GB virtual disk (as shown in VM evidence) |
| Networking | NAT and Host-only (`vboxnet0`) adapters are shown; isolation still needs verification |
| AD services | AD DS and DNS roles; promoted as the first Domain Controller |

## Techniques and Tools

- Oracle VirtualBox for the server VM and virtual networking
- Windows Server and Server Manager for initial configuration and role installation
- AD DS Configuration Wizard for forest creation and Domain Controller promotion
- DNS forward-lookup checks for the domain and Domain Controller

## Methodology

1. Prepared the Windows Server VM, set the hostname to `AllSafeCS-DC01`, checked updates and time zone, assigned the host-only static address, and enabled Remote Desktop.
2. Installed the AD DS and DNS server roles.
3. Promoted the server as a Domain Controller and created the `allsafe.local` domain/forest.
4. Checked DNS resolution. The notes record an earlier lookup timeout and later successful forward lookups for the domain and Domain Controller to `192.168.56.10`.

## Findings

- The server was promoted successfully to a Domain Controller for `allsafe.local`.
- AD DS and DNS role installation and promotion are evidenced in the roadmap screenshots.
- Later DNS checks resolved the domain and Domain Controller to `192.168.56.10`; an earlier check timed out, so the successful result is recorded without hiding the troubleshooting history.
- An earlier adapter screenshot shows `8.8.8.8` as alternate DNS. Confirm the final DNS settings on the domain-facing adapter and use the Domain Controller as the lab clients' DNS resolver.
- Both NAT and Host-only adapters appear in the server VM evidence. Verify the intended isolation and firewall exposure before further testing or publishing the lab.

## Screenshots

The relevant Windows Server, AD DS, domain promotion, and DNS evidence images are included in [Lab-01-Windows-Server-and-AD-DS-Deployment-Lab-Shots](https://github.com/te7mina1/Enterprise-Active-Directory-Environment/tree/main/Lab-01-Windows-Server-and-AD-DS-Deployment/Lab-Shots)

## Lessons Learned

- A stable server address, correct time configuration, and DNS setup are foundational to AD DS deployment.
- Installing the role is not enough: verify the promoted domain and perform DNS lookups, while documenting failures and subsequent successful checks.
- Confirm adapter isolation and final DNS resolver settings rather than assuming the lab network is isolated or correctly configured.

## Conclusion

The Windows Server setup, AD DS/DNS installation, `allsafe.local` domain creation, Domain Controller promotion, and DNS checks are documented with roadmap evidence. Final confirmation of the alternate DNS setting and NAT/Host-only isolation remains a follow-up before describing the lab as fully isolated or hardened.
