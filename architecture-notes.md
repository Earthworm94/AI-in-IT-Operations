# Architecture Notes
## K-12 Copilot Helpdesk Agent — Design Decisions & Rationale

---

## Why Microsoft Copilot Studio?

K-12 districts are overwhelmingly Microsoft shops. The average district already pays for M365 licensing, has Entra ID managing identity, and runs SharePoint as the intranet. Copilot Studio is the natural AI layer because:

- **No new vendor relationships** — lives inside the existing Microsoft tenant
- **Entra ID native** — identity is inherited, not bolted on
- **Power Automate integration** — connects to existing ticketing systems without custom code
- **Teams deployment** — staff are already there; no new app to install
- **FERPA alignment** — Microsoft's DPA for education covers Copilot Studio

Alternatives evaluated and deprioritized for this use case:

| Platform | Reason Deprioritized |
|---|---|
| ServiceNow Virtual Agent | Requires ServiceNow license; overkill for smaller districts |
| Google Dialogflow | Not viable in Microsoft-primary environments |
| Custom LangChain build | Requires engineering resources districts don't have |
| Freshdesk Freddy AI | Limited identity integration with Entra ID |

---

## Why Azure OpenAI (GPT-4o) as the Backend?

Copilot Studio supports multiple generative AI backends. GPT-4o was selected because:

- Data stays within the **Microsoft Azure boundary** — critical for FERPA
- **No opt-out required** for training data — Microsoft's education agreement covers this
- Strong performance on **technical troubleshooting** and **procedural guidance**
- Native integration — no API keys to manage, no third-party data processors

---

## Identity-First Design Principle

Most helpdesk chatbots are anonymous or use a shared login. This agent is designed **identity-first**:

- Every conversation is tied to an authenticated Entra ID user
- The agent **knows who it's talking to** before the first message
- Responses are role-scoped — a staff member cannot request admin-level actions
- Sensitive actions (account unlocks, permission changes) require **MFA step-up**

This mirrors Zero Trust principles: never trust, always verify, least privilege.

---

## Knowledge Base Architecture Decision

Two options were evaluated for grounding the agent's responses:

**Option A: SharePoint-native KB (Selected)**
- District already maintains SOPs and KB articles in SharePoint
- Copilot Studio natively indexes SharePoint via Microsoft Graph
- No data duplication — single source of truth
- Permissions inheritance — agent can only surface documents the user already has access to

**Option B: Dataverse Knowledge Base**
- More structured, better for complex topic trees
- Requires manual content migration
- Better for future agentic workflows

**Decision:** Start with SharePoint for speed and simplicity. Migrate to Dataverse in Phase 2 if topic complexity demands it.

---

## Escalation Design Philosophy

The agent is not designed to handle everything. It is designed to:

1. **Resolve** what it can confidently resolve (Tier 1)
2. **Escalate gracefully** when it cannot — with full context handed to the technician
3. **Never leave a user stuck** — every dead end routes to a human

Escalation triggers:
- Agent confidence score below threshold (< 0.7)
- User explicitly requests a human
- Issue flagged as security-related (account compromise, phishing)
- Three failed resolution attempts on same topic

When escalating, the agent passes:
- User identity (from Entra ID)
- Full conversation transcript
- Issue category and attempted resolutions
- Suggested ticket priority

---

## What This Architecture Does NOT Do

Being explicit about scope boundaries is important for governance:

- ❌ Does not have write access to Active Directory (read-only identity lookup only)
- ❌ Does not process student data — staff support only
- ❌ Does not store conversation history beyond session (privacy by design)
- ❌ Does not make autonomous changes to infrastructure
- ❌ Does not replace Tier 2/3 technician judgment

---

## Future Architecture Considerations

| Capability | Timeline | Dependency |
|---|---|---|
| Proactive outage notifications | Phase 3 | Azure Monitor integration |
| Ticket auto-creation in ServiceNow | Phase 2 | Power Automate connector |
| Voice channel via Teams Phone | Phase 4 | Teams Phone licensing |
| Student-facing variant | Future | Separate agent, stricter FERPA controls |
| Predictive issue detection | Future | Log Analytics + AI anomaly detection |
