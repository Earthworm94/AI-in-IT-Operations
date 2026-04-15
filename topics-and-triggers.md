# Agent Topics & Triggers
## K-12 Copilot Helpdesk Agent — What the Agent Handles

---

## Topic Design Principles

Each topic is designed around three questions:
1. **Can this be resolved without a human?** (If yes, build it)
2. **Is the resolution safe to automate?** (If no, escalate)
3. **Does the user need to feel heard?** (Always — tone matters)

---

## Topic Inventory

### 🔑 Category 1: Account & Identity

| Topic | Trigger Phrases | Resolution Type | Escalate If |
|---|---|---|---|
| Password Reset | "reset my password", "can't log in", "password expired", "locked out" | Self-service via SSPR link + guided steps | Account flagged, MFA not set up |
| MFA Setup | "set up MFA", "authenticator app", "two-factor", "verification code" | Guided walkthrough + KB article | User has no registered device |
| Account Lockout | "account locked", "too many attempts", "can't access my account" | Verify identity, provide unlock steps | Suspected security incident |
| SSO / App Access | "can't access [app]", "Single Sign-On not working", "login loop" | App-specific troubleshooting steps | Backend SSO config issue |
| New Staff Account | "I'm new", "account not set up", "haven't received login" | Provisioning checklist + IT escalation | Account not found in Entra ID |
| Guest/Vendor Access | "need access for a visitor", "contractor login" | Policy guidance + escalation to admin | Always escalates — requires approval |

---

### 💻 Category 2: Device Support

| Topic | Trigger Phrases | Resolution Type | Escalate If |
|---|---|---|---|
| Laptop Won't Start | "computer won't turn on", "black screen", "won't boot" | Guided troubleshooting (power, battery, hard reset) | Hardware failure suspected |
| Slow Performance | "computer is slow", "running sluggish", "takes forever to load" | Restart guidance, disk cleanup, background apps | Malware suspected |
| Printer Setup | "add a printer", "printer not showing up", "can't print" | Network printer install steps by campus | Driver issue, non-standard printer |
| Peripheral Issues | "mouse not working", "keyboard broken", "monitor flickering" | Basic troubleshooting, swap recommendation | Physical damage |
| Device Assignment | "I need a laptop", "my device was replaced", "loaner device" | Escalates to site tech with request logged | Always requires human approval |
| Chromebook Issues | "Chromebook won't sign in", "Chromebook update failed" | Google admin console guidance | MDM enrollment issue |

---

### 📧 Category 3: Microsoft 365

| Topic | Trigger Phrases | Resolution Type | Escalate If |
|---|---|---|---|
| Outlook Issues | "email not working", "can't send email", "Outlook won't open" | Step-by-step troubleshooting, re-profile steps | Mailbox corruption |
| Teams Issues | "Teams not working", "can't join meeting", "audio not working in Teams" | Audio/video settings, client reinstall steps | Backend Teams policy |
| SharePoint Access | "can't access SharePoint", "permission denied", "site not loading" | Permission check steps, request access flow | Site collection admin needed |
| OneDrive Sync | "OneDrive not syncing", "files not uploading", "sync error" | Sync troubleshooting, re-link steps | Storage quota exceeded |
| M365 App Licensing | "app not licensed", "subscription error", "Office not activated" | License assignment check + escalation | License not assigned in tenant |
| Teams Meeting Setup | "how do I schedule a meeting", "share my screen", "record a meeting" | How-to guidance from KB | N/A — informational only |

---

### 🌐 Category 4: Network & Access

| Topic | Trigger Phrases | Resolution Type | Escalate If |
|---|---|---|---|
| Wi-Fi Connection | "can't connect to Wi-Fi", "no internet", "keeps dropping" | SSID selection, forget/reconnect steps | Infrastructure issue |
| VPN Access | "VPN not connecting", "remote access not working" | VPN client steps, credential verification | Certificate issue, backend config |
| Campus Network | "network drive not showing", "can't access shared folder" | Drive mapping steps, credential refresh | GPO or DNS issue |
| Blocked Website | "website is blocked", "filter blocking my site" | Content filter policy explanation, request process | Requires admin override |
| Internet Speed | "internet is slow", "buffering", "video calls freezing" | Local troubleshooting, bandwidth guidance | Infrastructure issue |

---

### 🧑‍🏫 Category 5: New Staff Onboarding

| Topic | Trigger Phrases | Resolution Type | Escalate If |
|---|---|---|---|
| First Day Setup | "I just started", "what do I need to set up", "new employee IT" | Full onboarding checklist walkthrough | Account not provisioned |
| Software Access | "how do I get [software]", "I need access to [app]" | Approved software list + request process | Requires purchase or approval |
| Training Resources | "where do I learn [tool]", "Teams training", "how to use SharePoint" | Links to district KB, Microsoft Learn | N/A |
| Badge/Physical Access | "my badge doesn't work", "room access" | Redirect to facilities/HR | Out of IT scope |

---

## Fallback & Catch-All Behavior

When no topic matches:

1. Agent acknowledges it didn't understand
2. Offers top 4 most common topic buttons
3. Offers "Talk to a technician" option
4. If user selects technician: collects name, site, brief description → creates ticket → confirms to user

**Sample fallback message:**
> "I'm not sure I caught that — I want to make sure I get you the right help. Here are some things I can help with:"
> [Password Reset] [Device Issue] [Microsoft 365] [Something Else]
> Or I can connect you directly with your site technician.

---

## Out of Scope (Agent Declines Gracefully)

The agent is trained to recognize and redirect — not attempt — the following:

- Student data or grade inquiries → "That's outside my scope. Please contact your site admin."
- HR or payroll questions → "I handle IT support only. For HR, please contact [HR contact]."
- Security incidents (phishing, ransomware) → Immediate escalation + incident response trigger
- Personal device support → "I support district-issued devices only."
