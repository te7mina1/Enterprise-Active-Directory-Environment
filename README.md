# Enterprise-Active-Directory-Environment

## Overview

This repository documents my hands-on journey building and expanding an Enterprise Active Directory environment using Oracle VirtualBox, Windows Server, Windows 11, and Kali Linux.

The project is designed to simulate a small enterprise Windows domain where I can explore Active Directory administration, identity and access management, Group Policy, authentication, security misconfigurations, penetration testing, and defensive monitoring.

Rather than building a domain controller and stopping there, I am developing the environment into a practical cybersecurity lab where I can understand how enterprise environments operate, how their attack surfaces can be assessed, and how suspicious activities can be monitored and investigated.

The project follows two complementary perspectives:

- **Red Team:** Understanding Active Directory attack surfaces, enumeration techniques, security weaknesses, and controlled attack simulations.

- **Blue Team:** Monitoring Windows activity, investigating security events, identifying misconfigurations, and developing detection and remediation practices.

> All security testing is intended for my own isolated lab environment.
---

## Project Objectives

- Build and manage a Windows Server-based Active Directory domain.
- Understand AD DS, DNS, Organizational Units (OUs), users, groups, and domain administration.
- Configure and evaluate Group Policy and Windows security settings.
- Explore Active Directory reconnaissance and enumeration techniques.
- Understand common Active Directory attack paths and security weaknesses.
- Integrate Sysmon and security solutions(wazuh or splunk) for endpoint monitoring and security investigations.
- Perform controlled security simulations and examine the resulting telemetry.
- Document findings, evidence, lessons learned, and remediation steps.

---
### Lab Environment

| Component | Configuration |
| --------- | ------------- |
| Hypervisor | Oracle VirtualBox |
| Domain <br> your preferred domain name | allsafe.local|
| Domain Controller <br> your preferred DC name | AllSafeCS-DC01|
| Server OS | Windows Server 2025 |
| Client OS | Windows 11 Pro 25H2 |

**Network note:** The server's configuration evidence shows NAT and Host-only adapters. The final isolation and routing configuration still requires verification. The environment should not be considered fully isolated until that review is complete.

---
## Lab Index and Status

| Lab | Directory | Description | Status |
| --- | --------- | ------------|--------|
| 01 | [Lab-01-Windows-Server-and-AD-DS-Deployment](https://github.com/te7mina1/Enterprise-Active-Directory-Environment/tree/main/Lab-01-Windows-Server-and-AD-DS-Deployment) | Windows Server setup, AD DS installation, domain promotion, and DNS | Completed |
| 02 | [Lab-02-Domain-Objects-and-Client-Integration](https://github.com/te7mina1/Enterprise-Active-Directory-Environment/tree/main/Lab-02-Domain-Objects-and-Client-Integration) | OUs, users, groups, and Windows client domain joining | Completed |
| 03 | Lab-04-Group-Policy-and-Security-Configuration | Group Policy configuration and security-baseline experiments | Completed |
| 04 | Lab-05-Service-Accounts-and-SPN-Experiments | Service identities and Service Principal Name exercises | Completed |
| 05 | Upcoming | - | - |

---
## Technologies and Tools

**Infrastructure and administration**
- Oracle VirtualBox
- Windows Server 2025
- Windows 11 Pro
- Active Directory Domain Services
- DNS
- Group Policy Management

**Security assessment and reconnaissance**
- Kali Linux
- Nmap
- dig
- ldapsearch
- Additional Active Directory enumeration tools as the project progresses

**Monitoring and investigation**
- Wazuh
- Sysmon (planned for endpoint integration)

---
## Documentation and Evidence

Not all lab directory will follow a consistent documentation format:

1. Overview — What the lab is about.
2. Objectives — What I intend to achieve.
3. Environment and prerequisites — Required systems and configurations.
4. Implementation — Steps, commands, and configurations used.
5. Verification and results — Evidence that the task worked.
6. Screenshots — Supporting images stored in Lab-Shots/.
7. Lessons learned — Challenges, troubleshooting, and observations.
8. Security considerations — Identified risks and recommended improvements.

---
## Security Considerations

- All testing is performed against systems I own or am explicitly authorized to assess.
- Domain services should not be exposed directly to the public internet.
- VirtualBox network isolation and DNS configuration must be reviewed before further testing.
- Intentional security weaknesses are used only for controlled educational exercises.
- Unsafe Group Policy experiments, including disabling Microsoft Defender Antivirus, must be reviewed and reverted when no longer required.
- Privileged group memberships and service-account configurations must be reviewed.

---
## Project Status

**Active development.**

The foundational Active Directory environment has been deployed, including the Windows Server domain controller, AD DS, DNS, initial directory objects, and a joined Windows 11 client.

Progress still loading...

<!---I have also started investigating the domain controller's exposed services and DNS records as part of the Active Directory reconnaissance phase.--->

Future work will expand the environment into a practical Red Team and Blue Team lab, incorporating endpoint monitoring, controlled attack simulations, security investigations, detection development, and remediation.

---

## Author

**te7mina1**

Cybersecurity Student | SOC Analyst | Systems Administrator | Ethical Hacker

---
Building, testing, understanding, and securing enterprise Active Directory environments through hands-on cybersecurity practice.
