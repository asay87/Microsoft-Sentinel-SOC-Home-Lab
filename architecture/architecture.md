# SOC Home Lab – Architecture

## 1. SOC Objective
The objective of this project is to build a Security Operations Center (SOC) Home Lab designed to demonstrate hands-on skills in security log collection, threat detection, incident investigation, and incident response within a Microsoft Azure environment.

This lab aims to replicate core SOC operations using cloud-native security tools and best practices.

---

## 2. Project Scope
This project is implemented within a **single Azure tenant** dedicated to SOC activities, using an **Azure Free subscription** where applicable.

### Included services:
- Microsoft Sentinel (SIEM / SOAR)
- Log Analytics Workspace
- Microsoft Entra ID
- Windows Virtual Machine (endpoint simulation)
- Azure networking components (NSG / Firewall – basic level)
- Endpoint security tooling (Defender for Endpoint – lab context)

### Excluded services:
- On-premises infrastructure
- Advanced network appliances
- Large-scale production workloads

---

## 3. Architecture Overview
Security events are collected from Microsoft Entra ID and a Windows endpoint.  
All logs are centralized within a Log Analytics Workspace, where Microsoft Sentinel performs correlation, detection, and incident generation.

This centralized architecture reflects a simplified cloud-based SOC model.

*(Architecture diagram attached)*

---

## 4. Technical Components
- **Resource Group**: `rg-soc-homelab`
- **Log Analytics Workspace**: `law-soc-homelab`
- **Microsoft Sentinel**: SIEM / SOAR platform
- **Microsoft Defender for Endpoint**: Endpoint threat visibility
- **Microsoft Intune**: Endpoint management (if applicable)
- **Microsoft Entra ID**: Identity and authentication management
- **Windows Virtual Machine**: Simulated user endpoint
- **Azure Monitor Agent (AMA)**: Log collection agent

---

## 5. Log Sources

### Identity Logs (Entra ID)
- SignInLogs
- AuditLogs

### Endpoint Logs (Windows VM)
- Security Events:
  - 4624 – Successful logon
  - 4625 – Failed logon
  - 4688 – Process creation

These logs provide visibility into authentication behavior, system activity, and potential attack indicators.

---

## 6. Data Flow
1. Microsoft Entra ID generates authentication and audit logs  
2. The Windows VM generates security events  
3. Logs are forwarded to the Log Analytics Workspace  
4. Microsoft Sentinel analyzes and correlates events  
5. Security incidents are generated and tracked within Sentinel

---

## 7. Security & Best Practices
- Principle of least privilege applied to Azure roles
- Dedicated resource group for SOC components
- No secrets or sensitive identifiers stored in Git
- All screenshots are sanitized (IP addresses, UPNs, tenant IDs)
- Separation between monitoring and administration roles

---

## 8. Lab Limitations
- Limited log volume compared to production SOCs
- Single endpoint and single tenant
- No advanced threat intelligence feeds
- No automated containment actions enabled by default

---

## 9. Future Improvements
- Integration of additional log sources (network, firewall, NSG)
- Advanced KQL threat hunting scenarios
- More complex SOAR playbooks (containment, user disablement)
- Multi-tenant or cross-subscription log ingestion

---

## 10. Visual Evidence
- Microsoft Sentinel Overview screenshot
- Log Analytics Workspace configuration
- Architecture diagram
- Sample incident investigation screenshots
