# Success Metrics & ROI Framework
## K-12 Copilot Helpdesk Agent

---

## Measurement Philosophy

> "If you can't measure it, you can't present it to a school board."

This framework provides IT leaders with the data to demonstrate value, justify continued investment, and make the case for expanding AI capabilities across the district.

---

## Primary KPIs

### 1. Tier 1 Deflection Rate
**Definition:** Percentage of Tier 1 support interactions resolved by the agent without human intervention.

**Target:** ≥ 60% by end of Phase 3

**How to measure:** Copilot Studio Analytics → Resolved sessions / Total sessions

**Why it matters:** This is the headline ROI metric. Every deflected ticket = technician time reclaimed.

---

### 2. Mean Time to Resolution (MTTR)
**Definition:** Average time from user opening the agent to issue resolved or ticket created.

**Target:** ≤ 5 minutes for self-service resolutions

**Baseline (before agent):** ~45 minutes average for Tier 1 tickets (phone/email/walk-in)

**How to measure:** Copilot Studio session duration analytics

---

### 3. Agent CSAT (Customer Satisfaction)
**Definition:** Post-interaction satisfaction score collected via in-agent survey.

**Target:** ≥ 4.0/5.0

**Survey prompt:** "Did the IT Helpdesk Agent help you today?" [1–5 stars + optional comment]

**How to measure:** Copilot Studio built-in satisfaction surveys

---

### 4. Escalation Accuracy
**Definition:** Percentage of escalations that were correctly routed to the right technician/tier.

**Target:** ≥ 90%

**How to measure:** Technician feedback survey after each escalation ("Was this escalation appropriate?")

---

### 5. Knowledge Base Coverage
**Definition:** Percentage of agent interactions where a relevant KB article was found and surfaced.

**Target:** ≥ 80%

**How to measure:** Copilot Studio → Topics triggered vs. fallback/escalation rate

---

### 6. Adoption Rate
**Definition:** Percentage of eligible staff who have used the agent at least once per month.

**Target:** ≥ 50% by end of Phase 3, ≥ 70% by end of Phase 4

**How to measure:** Copilot Studio unique users / Total staff in Entra ID groups

---

## ROI Calculation Model

### Inputs (Customize for Your District)

| Variable | Example Value | Your Value |
|---|---|---|
| Total staff | 500 | |
| Average Tier 1 tickets per staff per month | 1.2 | |
| Total Tier 1 tickets per month | 600 | |
| Average technician hourly cost (loaded) | $35/hr | |
| Average Tier 1 resolution time (before agent) | 45 min | |
| Copilot Studio license cost per month | ~$200 (tenant) | |

### Monthly ROI Calculation

```
Monthly Tier 1 ticket volume:        600 tickets
Agent deflection rate (60%):         360 tickets deflected
Technician time saved per ticket:    45 min = 0.75 hrs
Total technician hours saved:        360 × 0.75 = 270 hrs/month
Technician cost savings:             270 × $35 = $9,450/month

Annual savings:                      $9,450 × 12 = $113,400/year
Annual Copilot Studio cost:          ~$2,400/year
Net annual ROI:                      ~$111,000
ROI ratio:                           47:1
```

> **Note:** This model is conservative. It does not account for after-hours support value, staff productivity gains from faster resolution, or reduced technician burnout.

---

## Monthly Reporting Dashboard

Recommended metrics for monthly IT leadership report:

| Metric | This Month | Last Month | Trend |
|---|---|---|---|
| Total agent interactions | | | |
| Tier 1 deflection rate | | | |
| Avg. resolution time | | | |
| CSAT score | | | |
| Tickets escalated to humans | | | |
| Top 5 topics by volume | | | |
| KB articles most accessed | | | |
| Technician hours saved (est.) | | | |
| Estimated cost savings | | | |

---

## Qualitative Success Indicators

Numbers tell part of the story. Also track:

- **Staff feedback themes** — Are staff satisfied? What's frustrating them?
- **Technician sentiment** — Are techs finding escalations well-prepared?
- **After-hours usage** — Is the 24/7 availability being used? (indicates real value)
- **New use case requests** — What are staff asking the agent that it can't yet handle? (roadmap fuel)

---

## Reporting Cadence

| Report | Audience | Frequency |
|---|---|---|
| Agent analytics summary | IT Manager | Weekly (automated) |
| Deflection & CSAT dashboard | IT Director | Monthly |
| ROI & business case report | Superintendent / Board | Quarterly |
| Security & compliance review | IT Security Lead | Monthly |
| KB gap analysis | IT team | Monthly |
