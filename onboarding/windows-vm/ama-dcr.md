# Windows VM Onboarding – Azure Monitor Agent (AMA) & Data Collection Rule (DCR)

## Objective
The purpose of this step is to onboard a Windows endpoint into the SOC environment by collecting Windows Security Events and forwarding them to the Log Analytics Workspace for analysis in Microsoft Sentinel.

Endpoint logs are essential for detecting local authentication failures, suspicious process execution, and potential compromise attempts.

---

## Endpoint Overview
A Windows virtual machine is deployed to simulate a user endpoint within the SOC environment.

**VM Role:**
- Simulated user workstation
- Source of operating system security events

**VM Name:**
- vm-win-soc-01

![Windows VM Overview](../../screenshots/onboarding/windows-vm/vm-overview.png)

---

## Azure Monitor Agent (AMA)

### Description
Azure Monitor Agent (AMA) is used to collect telemetry and security events from the Windows VM.  
AMA replaces the legacy Microsoft Monitoring Agent (MMA) and relies on Data Collection Rules for configuration.

### Installation
The Azure Monitor Agent is installed as a VM extension.

![Azure Monitor Agent Installed](../../screenshots/onboarding/windows-vm/ama-installed.png)

### SOC Relevance
- Centralized and scalable log collection
- Fine-grained control using Data Collection Rules
- Required for modern Microsoft Sentinel deployments

---

## Data Collection Rule (DCR)

### Purpose
The Data Collection Rule defines **what data is collected**, **from which machine**, and **where it is sent**.

### Configuration Overview
- **Scope**: vm-win-soc-01
- **Destination**: Log Analytics Workspace (`law-soc-homelab`)
- **Data source**: Windows Security Events

![DCR Overview](../../screenshots/onboarding/windows-vm/dcr-overview.png)

---

## Security Events Collected

The following Windows Security Event IDs are collected:

| Event ID | Description | SOC Value |
|--------|-------------|-----------|
| 4624 | Successful logon | User activity tracking |
| 4625 | Failed logon | Brute force detection |
| 4688 | Process creation | Suspicious process analysis |

These events provide visibility into authentication behavior and process execution on the endpoint.

---

## Validation

Log ingestion is validated using KQL queries in Microsoft Sentinel.

```kql
SecurityEvent
| where EventID == 4625
| take 10

