# Virtual Machines

This document describes the virtual machines used in the Sebbeco Enterprise Home Lab.

## Domain Controller – DC01

| Setting | Value |
|---|---|
| Operating System | Windows Server 2025 Standard Evaluation |
| Hostname | DC01 |
| IP Address | 192.168.10.10 |
| RAM | 3 GB |
| CPU | 2 vCPU |
| Disk | 80 GB |
| Role | Active Directory Domain Services and DNS |

## Client Workstation – CLIENT01

| Setting | Value |
|---|---|
| Operating System | Windows 11 Pro |
| Hostname | CLIENT01 |
| IP Address | 192.168.10.20 |
| RAM | 4 GB |
| CPU | 2 vCPU |
| Disk | 64–80 GB |
| Role | Domain-connected client workstation |

## SIEM Server – WAZUH01

| Setting | Value |
|---|---|
| Operating System | Ubuntu Server 24.04.5 LTS |
| Hostname | WAZUH01 |
| IP Address | 192.168.10.30 |
| RAM | 8 GB |
| CPU | 4 vCPU |
| Disk | 80 GB |
| Role | Wazuh Manager, Indexer and Dashboard |

## Virtualization

- Hypervisor: VMware Workstation
- Network: Host-only (VMnet1)
- Network subnet: 192.168.10.0/24

## Purpose

The virtual machines simulate a small enterprise IT environment.

- DC01 provides centralized identity management through Active Directory Domain Services and DNS.
- CLIENT01 represents an employee workstation joined to the Active Directory domain.
- WAZUH01 provides centralized security monitoring and log analysis through Wazuh SIEM.

Together, these systems provide an environment for practising Windows and Linux administration, networking, endpoint monitoring and cybersecurity investigations.
