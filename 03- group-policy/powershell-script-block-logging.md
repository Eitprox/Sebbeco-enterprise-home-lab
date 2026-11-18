
# PowerShell Script Block Logging

## Overview

PowerShell Script Block Logging is a Windows security feature that records the contents of PowerShell scripts and commands executed on a system.

In the Sebbeco Enterprise Home Lab, this feature is enabled through Group Policy to improve visibility into PowerShell activity on domain-connected computers.

The collected events are forwarded to Wazuh for centralized security monitoring and analysis.

## GPO Configuration

| Setting | Value |
|---|---|
| GPO Name | GPO-Security-PowerShell-Logging |
| Linked OU | Sebbeco |
| Policy | Turn on PowerShell Script Block Logging |
| Configuration | Enabled |
| Windows Event ID | 4104 |
| Target Computer | CLIENT01 |

## Configuration Path

Computer Configuration → Policies → Administrative Templates → Windows Components → Windows PowerShell

The following policy was configured:

- Turn on PowerShell Script Block Logging: Enabled

The policy enables PowerShell to record script block contents in the Windows PowerShell Operational event log.

## Policy Deployment and Verification

The policy was deployed to CLIENT01 through Group Policy.

The following commands were used to update and verify the applied computer policies:

```powershell
gpupdate /force
gpresult /r /scope computer
```

The registry configuration was also checked:

```powershell
Get-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
```

The `EnableScriptBlockLogging` value was confirmed to be set to `1`.

## Event Log Verification

PowerShell Script Block Logging was tested on CLIENT01 using a simple PowerShell function:

```powershell
function Test-ScriptBlockLogging {
    Write-Output "Sebbeco Home Lab - Script Block Logging Test"
}

Test-ScriptBlockLogging
```

The test generated Windows PowerShell Operational Event ID 4104.

This confirmed that PowerShell script block contents were being recorded locally.

## Wazuh Integration

The Windows PowerShell Operational event channel was configured as a log source in the Wazuh agent configuration on CLIENT01.

The agent forwarded the PowerShell events to WAZUH01 for centralized monitoring.

Event ID 4104 was successfully observed in Wazuh, confirming that the events were collected and indexed.

## Security Purpose

PowerShell Script Block Logging improves visibility into PowerShell activity and can support investigations involving suspicious commands or scripts.

When combined with centralized log collection and detection rules in Wazuh, it provides additional visibility into endpoint activity.

## Skills Demonstrated

- Group Policy Management
- Windows security auditing
- PowerShell logging configuration
- Windows Event Log analysis
- Wazuh agent configuration
- Centralized security monitoring
