
# Remote Access and Subnet Routing

## Overview

The Sebbeco Enterprise Home Lab uses Tailscale to provide secure remote access to the isolated VMware network.

The setup allows a remote Linux Mint laptop to access the lab machines without connecting them directly to the home network or exposing their management services to the public internet.

The main Windows desktop acts as a subnet router between the Tailscale network and the VMware Host-only network.

## Network Architecture

| Component | Role |
|---|---|
| Linux Mint Laptop | Remote administration workstation |
| Windows Desktop | Tailscale subnet router and VMware host |
| VMware VMnet1 | Isolated virtual network |
| DC01 | Active Directory and DNS |
| CLIENT01 | Windows 11 domain workstation |
| WAZUH01 | Wazuh SIEM server |

### Lab Network

| Device | IP Address |
|---|---|
| VMware Host Adapter (VMnet1) | 192.168.10.1 |
| DC01 | 192.168.10.10 |
| CLIENT01 | 192.168.10.20 |
| WAZUH01 | 192.168.10.30 |
| Lab Subnet | 192.168.10.0/24 |

## Tailscale Configuration

Tailscale was installed on:

- Linux Mint laptop
- Windows desktop

Both devices were authenticated using the same Tailscale account.

The Windows desktop was configured as a subnet router to provide access to the VMware Host-only network.

### Subnet Route Configuration

The following subnet was advertised from the Windows desktop:

```text
192.168.10.0/24
```

The route was approved in the Tailscale administration console.

On Linux Mint, subnet route acceptance was enabled:

```bash
sudo tailscale set --accept-routes
```

This allows the laptop to access devices within the advertised subnet.

### Windows IP Forwarding

IP forwarding was enabled on the two Windows network interfaces required for routing:

- Tailscale
- VMware Network Adapter VMnet1

The configuration was applied using PowerShell:

```powershell
Set-NetIPInterface -InterfaceAlias "Tailscale" -AddressFamily IPv4 -Forwarding Enabled

Set-NetIPInterface -InterfaceAlias "VMware Network Adapter VMnet1" -AddressFamily IPv4 -Forwarding Enabled
```

The forwarding configuration was verified using:

```powershell
Get-NetIPInterface -AddressFamily IPv4 |
Format-Table InterfaceAlias, Forwarding
```

Both interfaces reported forwarding as enabled.

## Remote Administration

The following remote administration methods were configured and tested.

| System | Protocol | Access Method |
|---|---|---|
| DC01 | RDP | Remmina |
| CLIENT01 | RDP | Remmina |
| WAZUH01 | SSH | Linux Terminal |
| Wazuh Dashboard | HTTPS | Web Browser |

### Windows Remote Desktop

Remote Desktop was enabled on DC01 and CLIENT01.

Network Level Authentication (NLA) was kept enabled to require authentication before establishing a remote desktop session.

Connections were tested from Linux Mint using Remmina.

### Linux Server Access

SSH was used to access WAZUH01:

```bash
ssh wazuhadmin@192.168.10.30
```

The Wazuh Dashboard was accessed through HTTPS:

```text
https://192.168.10.30
```

## Connectivity Verification

Several tests were performed to verify routing and remote access.

### Routing Verification

On Linux Mint:

```bash
ip route get 192.168.10.20
```

The result showed that traffic to CLIENT01 was routed through the Tailscale interface:

```text
192.168.10.20 dev tailscale0
```

The normal default internet route remained on the laptop's Wi-Fi interface.

### Network Connectivity

Connectivity was tested against all three virtual machines:

| Destination | Address | Result |
|---|---|---|
| DC01 | 192.168.10.10 | Successful |
| CLIENT01 | 192.168.10.20 | Successful |
| WAZUH01 | 192.168.10.30 | Successful |

### Firewall Troubleshooting

During testing, CLIENT01 did not initially respond to ICMPv4 echo requests.

The Windows Firewall configuration was inspected using PowerShell.

The Domain-profile inbound ICMPv4 echo-request rule was enabled:

```powershell
Enable-NetFirewallRule -Name "FPS-ICMP4-ERQ-In-NoScope"
```

Connectivity was subsequently verified using ping from Linux Mint.

Windows Firewall remained enabled.

## Security Considerations

The remote access configuration was designed to limit exposure of the home network.

The following security measures were implemented:

- Only the VMware lab subnet (`192.168.10.0/24`) is advertised through Tailscale.
- The home LAN is not advertised as a subnet route.
- The default internet route is not advertised through Tailscale.
- RDP and SSH are accessed through the private Tailscale connection.
- Network Level Authentication is enabled for Windows Remote Desktop.
- Windows Firewall remains enabled.
- Credentials and authentication secrets are not included in this repository.

## Skills Demonstrated

- VPN deployment and configuration
- Tailscale subnet routing
- IPv4 routing and IP forwarding
- Windows network administration
- Linux network troubleshooting
- Windows Firewall management
- Remote Desktop administration
- SSH administration
- Secure remote access design
