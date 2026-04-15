# Rollout Plan
## K-12 Copilot Helpdesk Agent — Phased District Deployment

---

## Deployment Philosophy

> "Big bang rollouts fail. Phased deployments with feedback loops succeed."

This plan follows a **crawl → walk → run** model across 4 phases. Each phase has defined entry criteria, success metrics, and exit criteria before proceeding to the next.

---

## Pre-Deployment Checklist

Before Phase 1 begins, confirm:

- [ ] Microsoft Copilot Studio license provisioned for tenant
- [ ] Azure OpenAI Service enabled in tenant (or GPT model configured in Copilot Studio)
- [ ] Entra ID security groups created (`AI-Helpdesk-Staff`, `AI-Helpdesk-SiteTech`, `AI-Helpdesk-Admin`)
- [ ] Conditional Access policy `CA-AI-Helpdesk-Agent-Access` created and tested
- [ ] SharePoint KB site created and initial articles published (minimum 20 articles)
- [ ] Power Automate ticketing flow built and tested (end-to-end)
- [ ] IT staff trained on escalation queue and agent handoff
- [ ] Acceptable Use Policy reviewed by legal and approved by district leadership
- [ ] Communication plan drafted for pilot site staff

---

## Phase 1: Pilot (Weeks 1–4)

**Goal:** Validate core functionality with a small, forgiving audience.

**Scope:**
- 1 site (recommend district office or most tech-savvy campus)
- 50–75 staff members
- Topics enabled: Password Reset, Account Lockout, Teams Issues, Ticket Submission only

**Deployment Channel:** Microsoft Teams (personal app)

**Success Criteria:**
- Agent successfully authenticates 100% of users via Entra ID SSO
- ≥ 70% of interactions reach a resolution or escalation (no dead ends)
- Zero security incidents attributable to the agent
- Pilot staff complete feedback survey (target: 80% response rate)

**Key Activities:**
- Week 1: Deploy to pilot group, send welcome communication
- Week 2: Daily monitoring of conversation analytics
- Week 3: First feedback collection, topic refinements
- Week 4: Pilot retrospective, go/no-go decision for Phase 2

**Exit Criteria for Phase 2:**
- Resolution rate ≥ 65%
- No critical bugs or security issues
- IT team comfortable with escalation workflow

---

## Phase 2: Expansion (Weeks 5–10)

**Goal:** Scale to multiple sites with full topic set.

**Scope:**
- 3 sites (pilot site + 2 additional)
- All staff at selected sites (~150–250 staff)
- Full topic set enabled (all 5 categories)
- Power Automate ticketing integration live

**Deployment Channels:** Microsoft Teams + SharePoint intranet widget

**New Capabilities Added:**
- Full device support topics
- Network troubleshooting topics
- New staff onboarding flow
- Automated ticket creation in [ServiceNow/Freshdesk]

**Success Criteria:**
- Tier 1 ticket volume to human technicians reduced by ≥ 40% at pilot site
- Agent CSAT score ≥ 3.5/5.0
- Escalation handoff working correctly 100% of time
- Average resolution time for self-service topics ≤ 5 minutes

**Key Activities:**
- Week 5: Expand Entra ID group membership, deploy to new sites
- Week 6–7: Monitor multi-site analytics, address site-specific KB gaps
- Week 8: Mid-expansion review with IT leads
- Week 9–10: Refinements, prepare Phase 3 communications

---

## Phase 3: District-Wide (Weeks 11–16)

**Goal:** Full district deployment with analytics and optimization.

**Scope:**
- All sites (8 campuses)
- All staff (~500 employees)
- Full feature set
- Analytics dashboard live for IT leadership

**Deployment Channels:** Teams + SharePoint + standalone web chat (for non-Teams users)

**New Capabilities Added:**
- Analytics dashboard (Copilot Studio + Power BI)
- Monthly ROI reporting for district leadership
- Site-specific KB customization (each campus can have campus-specific articles)
- Proactive notifications (agent pushes known outage info to affected staff)

**Success Criteria:**
- ≥ 60% of Tier 1 tickets resolved without human intervention district-wide
- All 8 sites actively using the agent (≥ 50% of staff have interacted)
- IT Director receives monthly automated ROI report
- Zero data governance incidents

**Key Activities:**
- Week 11: District-wide launch communication (email + Teams announcement)
- Week 12: All-staff deployment, monitor for volume spikes
- Week 13–14: Site-specific tuning based on campus KB gaps
- Week 15: First district-wide analytics review
- Week 16: Phase 3 retrospective, Phase 4 planning

---

## Phase 4: Optimization (Ongoing)

**Goal:** Continuous improvement and capability expansion.

**Quarterly Activities:**
- KB article review and refresh (retire stale, add new)
- Topic performance review (identify low-resolution topics for redesign)
- User feedback analysis and agent tuning
- Security review of Conditional Access policies and Graph permissions
- ROI reporting to district leadership

**Potential Future Capabilities:**
| Capability | Dependency | Timeline |
|---|---|---|
| Proactive outage alerts | Azure Monitor integration | Q3 |
| Voice channel (Teams Phone) | Teams Phone licensing | Q4 |
| Student-facing variant (separate agent) | FERPA review, separate design | Future |
| Predictive issue detection | Log Analytics + AI | Future |
| Manager self-service (onboard/offboard requests) | Identity Governance | Future |

---

## Communication Templates

### Phase 1 Pilot Invite Email

> **Subject:** You're invited: AI IT Support Pilot
>
> Hi [Name],
>
> Your site has been selected to pilot our new AI IT Helpdesk, available directly in Microsoft Teams. Starting [date], you can get instant help with password resets, device issues, and Microsoft 365 support — 24/7, no wait time.
>
> **How to access:** Open Teams → Apps → Search "IT Helpdesk"
>
> Your feedback shapes how we roll this out district-wide. A short survey will be sent after your first interaction.
>
> Questions? Reply to this email or contact [IT contact].

---

### District-Wide Launch Email

> **Subject:** New: AI IT Support is now available to all staff
>
> We're excited to announce that AI-powered IT support is now available to all district staff.
>
> Get instant help — day or night — with:
> - Password resets and account issues
> - Device troubleshooting
> - Microsoft 365 support
> - And more
>
> **Access it in Teams:** [Instructions] or on the intranet at [URL]
>
> For complex issues, the agent will connect you directly with your site technician. You'll never be left without support.

---

## Rollout Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Low adoption at pilot site | Medium | Medium | Champion program — identify 2-3 enthusiastic early adopters per site |
| KB gaps causing poor resolution | High | Medium | Pre-launch KB audit, 20 article minimum before go-live |
| Staff distrust of AI | Medium | High | Transparent communication, easy human escalation always available |
| Entra ID group misconfiguration | Low | High | Test all role tiers before Phase 1 launch |
| Ticketing integration failure | Medium | Medium | Manual ticket fallback during Phase 1, integration required before Phase 2 |
