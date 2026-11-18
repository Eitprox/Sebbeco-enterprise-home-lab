
# Organizational Unit Structure

## Overview

Organizational Units (OUs) are used to organize users, groups and computers within Active Directory.

They provide a logical structure for directory objects and allow Group Policy Objects (GPOs) to be linked to specific departments or organizational units.

## OU Structure

The lab uses the following Organizational Unit structure:

```text
ad.Sebbeco.test
└── Sebbeco
    ├── IT
    ├── HR
    ├── Finance
    └── Management
```

## Department OUs

| Organizational Unit | Purpose |
|---|---|
| IT | IT staff, support accounts and domain-connected IT computers |
| HR | Human Resources employees |
| Finance | Finance department employees |
| Management | Management accounts |

## Object Placement

The following objects have been organized within the OU structure:

| Object | Organizational Unit |
|---|---|
| hr.test1 | Sebbeco/HR |
| it.admin1 | Sebbeco/IT |
| IT-Support | Sebbeco/IT |
| CLIENT01 | Sebbeco/IT |

## Group Policy Management

The OU structure provides a foundation for applying department-specific Group Policies.

For example:

- HR policies can be linked to the HR OU.
- IT policies can be linked to the IT OU.
- Computer accounts can be organized according to their administrative purpose.

## Purpose

This structure simulates a small enterprise where directory objects are organized according to departmental responsibilities.

It provides a foundation for:

- Centralized user and computer management.
- Department-specific Group Policy deployment.
- Delegated administration.
- Access control based on organizational roles.
