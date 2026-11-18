
# User and Group Management

## Overview

Active Directory user accounts and security groups are used to manage identities and simplify access administration in the Sebbeco Enterprise Home Lab.

Users are organized into department-specific Organizational Units (OUs), while security groups provide a centralized way to manage access to resources.

## User Accounts

The following test accounts have been created:

| Username | Department | Organizational Unit | Purpose |
|---|---|---|---|
| hr.test1 | HR | Sebbeco/HR | Test employee account |
| it.admin1 | IT | Sebbeco/IT | IT administration test account |

These accounts are used to represent different roles within the simulated enterprise environment.

## Security Groups

The following security group has been created:

| Group Name | Location | Purpose |
|---|---|---|
| IT-Support | Sebbeco/IT | Represents the IT support team |

Security groups can be used to assign permissions to multiple users through group membership rather than configuring permissions for each individual account.

## Implemented Tasks

- Created department-specific Active Directory user accounts.
- Organized user accounts into their respective Organizational Units.
- Created the IT-Support security group.
- Used the domain account `AD\hr.test1` to verify domain authentication on CLIENT01.
- Verified the secure channel between CLIENT01 and the domain controller using PowerShell.

## Why Use Security Groups?

Security groups simplify access management in an enterprise environment.

Instead of assigning permissions to individual users, administrators can assign permissions to a security group and manage access through group membership.

This improves consistency and makes administration easier as the organization grows.

## Security Considerations

- Use individual user accounts instead of shared accounts.
- Apply the principle of least privilege.
- Avoid using privileged accounts for everyday tasks.
- Use strong passwords and appropriate account policies.
- Review group membership and permissions regularly.
