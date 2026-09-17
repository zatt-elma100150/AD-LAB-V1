# 🌐 AD-LAB-V1
![VirtualBox](https://img.shields.io/badge/VirtualBox-Virtualization-183A61?logo=virtualbox&logoColor=white)
![Windows Server](https://img.shields.io/badge/Windows_Server-2022-0078D4?logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active_Directory-DS-blue?logo=microsoft&logoColor=white)
![Windows 11](https://img.shields.io/badge/Windows_11-Client-0078D4?logo=windows11&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-Client-E95420?logo=ubuntu&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

Personal Active Directory lab built with Oracle VirtualBox and Windows Server 2022.

This project demonstrates the deployment and management of an Active Directory domain environment, including multiple domain controllers, a Read-Only Domain Controller, DNS, DHCP, Group Policy Objects and domain-joined clients (Windows & Linux).

## Table of Contents

- [Objectives](#objectives)
- [Lab Environment](#lab-environment)
- [Architecture](#architecture)
- [Infrastructure](#infrastructure)
- [Group Policy Objects](#group-policy-objects)
- [Validation](#validation)
- [Tech Stack](#tech-stack)
- [Full Documentation](#full-documentation)
- [Screenshots](#screenshots)
- [Author](#author)

## Objectives

The main objectives of this project are:

- Deploy an Active Directory domain using Windows Server 2022.
- Configure DNS and DHCP services.
- Add a second domain controller for redundancy.
- Deploy and test a Read-Only Domain Controller (RODC).
- Join Windows 11 and Ubuntu virtual machines to the domain.
- Configure and validate Group Policy Objects.
- Configure DHCP Failover in Hot Standby mode.
- Document the architecture and validation procedures.

## Lab Environment

| Component | Details |
|---|---|
| Virtualization platform | Oracle VirtualBox |
| Domain | LAB.local |
| Network | 192.168.56.0/24 |
| Main server | DC01 – Windows Server 2022 |
| Secondary server | DC02 – Windows Server 2022 |
| Read-only controller | RODC01 – Windows Server 2022 |
| Windows client | Windows 11 |
| Linux client | Ubuntu |

## Architecture

The following diagram shows the VirtualBox network topology and the main services deployed in the lab.

### Diagram

![AD Lab Architecture Diagram](images/diagram.png)

## Infrastructure

### DC01

DC01 is the primary domain controller and provides the following services:

- Active Directory Domain Services
- DNS
- DHCP
- Active Directory Certificate Services
- Internet access through a NAT adapter

### DC02

DC02 is the secondary domain controller and provides redundancy for the domain environment:

- Active Directory Domain Services
- DNS
- DHCP
- Active Directory replication with DC01
- DHCP Failover in Hot Standby mode

### RODC01

RODC01 is a Read-Only Domain Controller configured with:

- Read-only Active Directory database
- DNS
- Password Replication Policy
- Internal network connectivity only

## Group Policy Objects

This lab includes nine custom GPOs and two default Active Directory policies. A Fine-Grained Password Policy was also configured separately for privileged accounts.

| GPO Name | Scope | Description |
|---|---|---|
| Advanced Auditing | LAB.local/Domain Controllers | Enables advanced security auditing on domain controllers, tracking logon events, account management, policy changes, and object access for compliance and incident investigation purposes. |
| AppLocker | LAB.local/_COMPUTERS | Enforces application whitelisting through AppLocker, restricting execution of unauthorized software and reducing the attack surface across domain-joined workstations. |
| BitLocker Recovery | LAB.local/Domain Controllers | Stores BitLocker recovery information in Active Directory for the targeted domain controller computer objects, allowing authorized administrators to retrieve recovery data centrally. |
| Control Panel Block | LAB.local/_USERS | Restricts standard users from accessing Control Panel and PC settings, preventing unauthorized changes to system configuration. |
| Corporate Wallpaper | LAB.local/_USERS | Applies a standardized desktop wallpaper through the NETLOGON share and prevents user-side modification. |
| Folder Redirection | LAB.local/_USERS | Redirects user profile folders (Desktop, Documents) to a centralized network location, ensuring data persistence independent of the local machine. |
| Map Network Drive | LAB.local/_USERS | Automatically maps a network drive at logon, providing users with consistent access to shared resources without manual configuration. |
| Password Policies | LAB.local | Enforces domain-wide password complexity, minimum length, expiration, and account lockout thresholds to strengthen credential security. |
| Restrict Software Installation | LAB.local/_USERS | Prevents standard users from installing unauthorized software, reducing the risk of malware introduction and maintaining endpoint compliance. |

### Default GPOs

| GPO Name | Scope | Description |
|---|---|---|
| Default Domain Policy | LAB.local | Baseline domain-wide policy automatically created by Active Directory, defining core password, lockout, and Kerberos authentication settings. |
| Default Domain Controllers Policy | LAB.local/Domain Controllers | Baseline security policy automatically applied to domain controllers, governing user rights assignment and default audit behavior. |

## Validation

The lab environment was tested to confirm that core services and policies behave as expected:

- Group Policy application verified on domain-joined clients using `gpupdate /force` and `gpresult /r`.
- DNS resolution tested for internal domain records and forward/reverse lookup zones using `nslookup` and `Resolve-DnsName`.
- DHCP Failover in Hot Standby mode validated between DC01 and DC02, confirming lease synchronization and automatic failover.
- Active Directory replication verified between DC01, DC02, and RODC01 using `repadmin /replsummary` and `repadmin /showrepl`.

> Full step-by-step validation procedures, command outputs, and screenshots are available in the full project documentation.

## Tech Stack

Windows Server 2022 · Windows 11 · Ubuntu · Active Directory Domain Services (AD DS) · DNS · DHCP · Group Policy Objects (GPO) · Read-Only Domain Controller (RODC) · Oracle VirtualBox

## Full Documentation

Detailed configuration steps, screenshots, and validation results are available in the full project documentation:

📄 

## Screenshots
Selected screenshots from the lab environment. Detailed configuration screenshots and validation evidence are available in the full project documentation.

### VirtualBox Lab Environment

![VirtualBox Lab Environment](images/VB.png)

VirtualBox Manager displaying the domain controllers and domain-joined client machines used in the lab.

### Active Directory Users and Computers

![Active Directory Users and Computers](images/ADCU.png)

Active Directory Users and Computers showing the domain controllers, including the Read-Only Domain Controller.

### Group Policy Management

![Group Policy Management](images/LAB01.png)

Group Policy Management displaying the configured domain and security-related Group Policy Objects.

### Windows 11 Domain-Joined Client

![Windows 11 Domain-Joined Client](images/Win11.png)

Windows 11 domain-joined client displaying the corporate wallpaper applied through Group Policy.

## Author

**M. El Majdoul** |
IT Support / Sysadmin enthusiast — Active Directory & Infrastructure Lab

🔗 [LinkedIn](https://www.linkedin.com/in/mohamed-e-4a7167146)

## License

© 2026 M. El Majdoul. All rights reserved. This project may not be copied, modified, or redistributed without permission.
