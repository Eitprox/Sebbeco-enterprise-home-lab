# Network Topology

This document describes the virtual network architecture used in the Sebbeco Enterprise Home Lab.

## Network Configuration

The lab uses an isolated Host-only network in VMware Workstation.

| Setting | Value |
|---|---|
| Network Type | Host-only |
| VMware Network | VMnet1 |
| Network Subnet | 192.168.10.0/24 |
| Host IP Address | 192.168.10.1 |

## Network Devices

| Device | Hostname | IP Address | Role |
|---|---|---|---|
| VMware Host | Host VMnet1 | 192.168.10.1 | Host access to the virtual network |
| Domain Controller | DC01 | 192.168.10.10 | Active Directory and DNS |
| Client Workstation | CLIENT01 | 192.168.10.20 | Domain-connected Windows client |
| SIEM Server | WAZUH01 | 192.168.10.30 | Centralized security monitoring |

## Network Architecture

All three virtual machines are connected to the same isolated Host-only network.

- DC01 provides Active Directory Domain Services and DNS.
- CLIENT01 is joined to the Active Directory domain and forwards Windows event logs to WAZUH01.
- WAZUH01 receives and analyses security events using Wazuh Manager.

## Purpose

The isolated network provides a controlled environment for practising enterprise networking, Windows and Linux administration, centralized identity management and cybersecurity monitoring.

The Host-only configuration keeps the lab network separate from the external network unless additional connectivity is deliberately configured.
