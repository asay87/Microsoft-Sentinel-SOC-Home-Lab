
# Entra ID – Diagnostic Settings Onboarding

## Objective
The purpose of this configuration is to enable the collection of Microsoft Entra ID logs and forward them to a Log Analytics Workspace in order to support security monitoring, threat detection, and incident investigation within Microsoft Sentinel.

Identity logs are a critical data source for any SOC as they provide visibility into authentication attempts and administrative activities.

---

## Logs Collected

### SignInLogs
These logs record authentication attempts to Entra ID–protected resources.

**Security value:**
- Detection of brute force attacks
- Identification of repeated failed sign-ins
- Analysis of suspicious login behavior
- Correlation with endpoint activity

**Common use cases:**
- Brute force detection
- Impossible travel analysis
- Unusual login patterns

---

### AuditLogs
These logs record changes made within Entra ID.

**Security value:**
- Tracking administrative actions
- Detecting privilege escalation attempts
- Monitoring changes to users, groups, and roles

**Common use cases:**
- Unauthorized role assignments
- Suspicious configuration changes
- Compliance and audit tracking

---

## Configuration Details
- **Log source**: Microsoft Entra ID
- **Destination**: Log Analytics Workspace (`law-soc-homelab`)
- **Collection method**: Diagnostic Settings
- **Logs enabled**:
  - SignInLogs
  - AuditLogs

---

## SOC Relevance
Entra ID logs enable the SOC to:
- Monitor authentication activity across the environment
- Detect identity-based attacks early
- Correlate identity events with endpoint security events
- Investigate incidents involving user compromise or misuse of privileges

These logs form the foundation of identity-centric detections in Microsoft Sentinel.

---

## Validation
Log ingestion is validated using KQL queries within Microsoft Sentinel:

```kql
SigninLogs
| take 10
