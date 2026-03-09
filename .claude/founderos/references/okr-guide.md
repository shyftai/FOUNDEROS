# OKR Guide

Reference for setting, tracking, and scoring OKRs. Load before running `/founder:okrs`.

---

## What makes a good Objective

- **Qualitative** — describes a desired outcome, not a metric
- **Inspiring** — motivates the team, not just measures them
- **Time-bound** — typically one quarter
- **Ambitious** — should feel challenging but not impossible
- **Aligned** — clearly supports the company vision

**Good objectives:**
- "Become the go-to platform for B2B sales teams"
- "Build a world-class engineering team"
- "Establish market leadership in our core segment"

**Bad objectives:**
- "Increase revenue by 30%" (this is a key result, not an objective)
- "Ship features" (not inspiring or specific)
- "Do marketing better" (vague)

---

## What makes a good Key Result

- **Measurable** — has a specific number or threshold
- **Outcome-based** — measures results, not activities
- **Time-bound** — achievable within the quarter
- **Ambitious** — target 0.6-0.7 average score (if you hit 1.0 every time, you're not stretching)
- **Limited** — 2-3 per objective (max 5)

**Good key results:**
- "Increase MRR from $50K to $75K"
- "Reduce customer churn from 8% to 4%"
- "Close 3 enterprise deals ($50K+ ACV)"
- "Achieve NPS score of 50+"

**Bad key results:**
- "Launch new feature" (activity, not outcome)
- "Talk to 20 customers" (input, not output)
- "Improve product" (not measurable)

---

## OKR scoring

| Score | Meaning | Interpretation |
|-------|---------|---------------|
| 1.0 | Fully achieved | Either excellent execution or the target was too easy |
| 0.7 | Strong progress | Hit the "stretch" zone — ideal OKR calibration |
| 0.5 | Meaningful progress | Moved the needle but significant gap to target |
| 0.3 | Some progress | Started but didn't get far — investigate blockers |
| 0.0 | No progress | Either deprioritized or fundamentally misjudged |

**Healthy average score: 0.6-0.7**
- Consistently 1.0 → OKRs not ambitious enough
- Consistently <0.4 → OKRs unrealistic or company has execution issues

---

## OKR cadence

| Activity | Frequency | When |
|----------|-----------|------|
| Set OKRs | Quarterly | Last 2 weeks of previous quarter |
| Track progress | Weekly | During /founder:weekly or /founder:today |
| Mid-quarter review | Once | Week 6-7 of quarter |
| Score and review | Quarterly | Last week of quarter |
| Annual planning | Yearly | Q4 or early Q1 |

---

## OKR alignment

```
Company Vision
    │
Company OKRs (2-3 objectives)
    │
    ├── Department OKR → GTM:OS metrics
    ├── Department OKR → FINANCE:OS metrics
    ├── Department OKR → HR:OS metrics
    └── Department OKR → CONTENT:OS / COMMUNITY:OS metrics
```

Every department/OS framework OKR should trace back to a company OKR. If it doesn't, ask why it exists.

---

## Common OKR mistakes

| Mistake | Why it's wrong | Fix |
|---------|---------------|-----|
| Too many OKRs | Dilutes focus | Max 3 objectives, 3 KRs each |
| KRs as tasks | Measures activity not outcome | Ask "So what?" — what does doing the task achieve? |
| Sandbagging | Easy targets that guarantee 1.0 | Raise targets until 0.7 feels like a stretch |
| No owner | Nobody is accountable | Every KR needs exactly one owner |
| Set and forget | No weekly tracking | Review in /founder:weekly every week |
| Changing mid-quarter | Moving goalposts | Only change if strategy fundamentally shifts |
| Confusing KPIs with OKRs | KPIs maintain; OKRs transform | OKRs should change the trajectory, not describe steady state |

---

## OKR examples by stage

### Pre-seed / Seed
- O: Validate product-market fit
  - KR: 10 customers using product weekly (up from 2)
  - KR: 50% of users return within 7 days
  - KR: 3 customers willing to pay $X/month

### Series A
- O: Build a repeatable sales engine
  - KR: Increase MRR from $30K to $80K
  - KR: Achieve 20% month-over-month pipeline growth
  - KR: Close 5 deals through outbound (proving GTM playbook)

### Growth
- O: Establish category leadership
  - KR: Reach $500K MRR
  - KR: Win 60% of competitive deals
  - KR: Achieve top-3 ranking in G2 category

---

## Mid-quarter adjustment protocol

At week 6-7, for each at-risk KR:
1. Is the target still relevant? (If strategy changed, adjust)
2. What's blocking progress? (Identify and remove blockers)
3. Can resources be reallocated? (From ahead KRs to behind ones)
4. What's the minimum viable progress by quarter-end?
5. Document the adjustment and rationale — never silently change targets
