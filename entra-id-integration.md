# Entra ID Integration
## K-12 Copilot Helpdesk Agent — Identity & Authentication Design

---

## Overview

This agent is designed with an **identity-first architecture**. Every interaction is bound to a verified Microsoft Entra ID (formerly Azure AD) identity before any support topic is surfaced.

This is not optional — it is foundational to the security posture, FERPA compliance, and role-based response design of the agent.

---

## Authentication Flow

```
User opens agent (Teams / SharePoint / Web)
          │
          ▼
[Entra ID SSO Challenge]
          │
    Already signed in? ──Yes──▶ Token passed silently
          │
          No
          ▼
[Interactive Login / MFA Prompt]
          │
          ▼
[Entra ID issues OAuth 2.0 token]
          │
          ▼
[Copilot Studio validates token]
          │
          ▼
[Agent retrieves user profile via Microsoft Graph]
    - Display name
    - Department
    - Job title
    - Site/campus (extension attribute)
    - Group memberships (for role determination)
          │
          ▼
[Role assigned → scoped topic set loaded]
          │
          ▼
[Conversation begins — agent greets by name]
```

---

## Role Definitions & Topic Scope

Roles are determined by **Entra ID Security Group membership**, not job title (job titles are inconsistent across districts).

| Role | Entra ID Group | Agent Capabilities |
|---|---|---|
| **Staff** | `AI-Helpdesk-Staff` | Self-service Tier 1 topics, ticket submission |
| **Site Technician** | `AI-Helpdesk-SiteTech` | All staff topics + escalation queue view + ticket management |
| **IT Admin** | `AI-Helpdesk-Admin` | All topics + sensitive actions + agent analytics |
| **New/Unprovisioned** | Not in any group | Limited to "I'm new" onboarding flow only |

> **Important:** Group membership is evaluated at session start. Changes take effect at next login.

---

## Sensitive Action Handling (Step-Up MFA)

Certain agent actions require additional identity verification beyond the initial login, even if the user is already authenticated. This follows the principle of **step-up authentication**.

Actions requiring step-up MFA:

| Action | Why |
|---|---|
| Initiating a self-service password reset | Confirms physical possession of registered device |
| Requesting elevated software access | Prevents social engineering via the agent |
| Viewing ticket history (own tickets) | PII protection |
| Submitting a security incident report | Ensures accountability |

Step-up is triggered via **Entra ID Conditional Access Authentication Strength** policies, not custom code.

---

## What the Agent Can Read (via Microsoft Graph)

The agent has **read-only** Microsoft Graph access scoped to the minimum required:

| Graph Permission | Scope | Purpose |
|---|---|---|
| `User.Read` | Delegated | Get authenticated user's profile |
| `GroupMember.Read.All` | Application | Determine role from group membership |
| `Sites.Read.All` | Application | Read KB articles from SharePoint |
| `MailboxSettings.Read` | Delegated | Check if user mailbox is provisioned |

**The agent has zero write permissions to Entra ID, Active Directory, or Exchange.**

All write actions (password resets, account unlocks) are performed by:
- The user themselves via SSPR (Self-Service Password Reset)
- A human technician after agent escalation
- A Power Automate flow with its own service account (separately permissioned and audited)

---

## Conditional Access Policy Integration

The agent is registered as an **Enterprise Application** in Entra ID. A dedicated Conditional Access policy governs access:

**Policy: `CA-AI-Helpdesk-Agent-Access`**

| Condition | Requirement |
|---|---|
| Users | Members of `AI-Helpdesk-Staff`, `AI-Helpdesk-SiteTech`, `AI-Helpdesk-Admin` |
| Device platforms | Windows, iOS, Android, macOS |
| Device compliance | Compliant (Intune-managed) OR Hybrid Azure AD Joined |
| Locations | Any (agent is available on and off campus) |
| Grant controls | Require MFA |
| Session controls | Sign-in frequency: 8 hours |

> **Note:** Non-compliant or unmanaged personal devices will be blocked and redirected to an enrollment guide.

---

## Audit & Logging

All agent interactions are logged for compliance purposes:

| Log Type | Location | Retention |
|---|---|---|
| Sign-in logs | Entra ID Sign-in Logs | 30 days (extend via Log Analytics) |
| Agent conversation metadata | Copilot Studio Analytics | 90 days |
| Sensitive action triggers | Microsoft Purview Audit | 1 year |
| Escalation events | ServiceNow / Ticketing system | Per district policy |

**No conversation content is retained** beyond the active session — privacy by design.

---

## FERPA Alignment Notes

- Agent only accesses **staff data** — student records are explicitly out of scope
- Microsoft Graph permissions are scoped to prevent access to student-related data stores
- All data processing occurs within the district's **Microsoft 365 tenant boundary**
- Microsoft's **Student Data Privacy Consortium (SDPC)** agreement and FERPA DPA covers Copilot Studio in licensed education tenants
- Agent cannot be queried by or about students under any configuration in this design

---

## Related Documents

- [Conditional Access Policy](./conditional-access-policy.md)
- [Data Classification](./data-classification.md)
- [FERPA Compliance Notes](../governance/ferpa-compliance-notes.md)
- [Incident Response](../governance/incident-response.md)
