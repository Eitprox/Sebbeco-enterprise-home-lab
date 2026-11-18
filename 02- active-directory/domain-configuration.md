
# Active Directory Domain Configuration

## Overview

Active Directory Domain Services (AD DS) is used to provide centralized identity and access management in the Sebbeco Enterprise Home Lab.

## Domain Information

| Setting | Value |
|---|---|
| Domain Name | ad.Sebbeco.test |
| NetBIOS Name | AD |
| Domain Controller | DC01 |
| Domain Controller IP | 192.168.10.10 |
| Operating System | Windows Server 2025 |

# Active Directory Domain Configuration

## Overview

Active Directory Domain Services (AD DS) provides centralized identity and access management in the Sebbeco Enterprise Home Lab.

The domain controller is responsible for managing domain authentication, directory services and DNS.

## Domain Information

| Setting | Value |
|---|---|
| Domain Name | ad.Sebbeco.test |
| NetBIOS Name | AD |
| Domain Controller | DC01 |
| Domain Controller IP | 192.168.10.10 |
| Operating System | Windows Server 2025 Standard Evaluation |

## Implemented Configuration

- Installed Active Directory Domain Services (AD DS).
- Installed and configured DNS Server.
- Promoted DC01 to a domain controller.
- Created the `ad.Sebbeco.test` domain.
- Configured CLIENT01 to use the domain controller for DNS.
- Joined CLIENT01 to the Active Directory domain.

## Domain Authentication and Verification

CLIENT01 successfully joined the domain and was used to verify domain authentication.

The domain user account `AD\hr.test1` was used to test domain login.

The computer's secure channel was also verified using PowerShell:

```powershell
Test-ComputerSecureChannel -Verbose
```

The command returned `True`, confirming that the secure channel between CLIENT01 and the domain was functioning correctly at the time of testing.

## Purpose

The domain provides centralized authentication and management of users and computers.

This setup simulates a small business IT infrastructure and provides a foundation for Group Policy management, access control and centralized security administration.

## Implemented Configuration

- Installed Active Directory Domain Services.
- Installed DNS Server.
- Promoted DC01 to a domain controller.
- Created the `ad.Sebbeco.test` domain.
- Configured DNS on the domain controller.
- Joined CLIENT01 to the domain.

## Domain Authentication

CLIENT01 successfully joined the domain.

A domain user account (`AD\hr.test1`) was used to verify that domain authentication works.

## Purpose

The domain provides centralized authentication and management of users and computers, simulating a small business IT infrastructure.
