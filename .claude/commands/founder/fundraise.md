Fundraising decision framework. Helps the founder decide IF, WHEN, and HOW MUCH to raise — then routes to INVESTOR:OS.

Display:
```
<< FOUNDER:OS // FUNDRAISE >>
```

Follow these steps:

1. Read VISION.md, OKRS.md, and pull data from FINANCE:OS and INVESTOR:OS
2. Assess the current situation:
   a. **Do you need to raise?**
      - Current runway from FINANCE:OS
      - Revenue trajectory — are you growing toward profitability?
      - If runway >18 months and revenue growing, challenge the need
   b. **Is now the right time?**
      - Are metrics strong enough? (Pull from GTM:OS, FINANCE:OS)
      - Is the market receptive? (Check INVESTOR:OS for recent activity)
      - Are you fundraising from strength or desperation?
   c. **How much?**
      - Calculate 18-24 month runway need at planned burn
      - Factor in hiring plan from HR:OS
      - Factor in growth investments from ROADMAP.md
      - Add 20% buffer
   d. **At what terms?**
      - Load BENCHMARKS.md for stage-appropriate valuation ranges
      - Review dilution implications
3. This is a **Type 1 decision** — run all six quality gates
4. Display the fundraise analysis:

```
  ┌─ FUNDRAISE ANALYSIS ────────────────────────────────────┐
  │                                                          │
  │  Current state:                                          │
  │    Runway:      {months} months                          │
  │    MRR:         ${amount} ({trend}% MoM)                 │
  │    Burn:        ${amount}/mo                             │
  │    Team:        {n} people                               │
  │                                                          │
  │  Raise recommendation:                                   │
  │    Raise:       {yes/no/not yet}                         │
  │    Amount:      ${amount}                                │
  │    Target close: {date}                                  │
  │    Use of funds: hiring ({%}), growth ({%}), runway ({%})│
  │                                                          │
  │  Readiness check:                                        │
  │  [x] Metrics support the story                           │
  │  [x] Pipeline has enough investors                       │
  │  [ ] Data room prepared                                  │
  │  [ ] Board aligned on terms                              │
  │                                                          │
  │  ── DECISION GATES ────────────────────────────────      │
  │  [x] Vision  [x] OKR  [x] Data  [ ] Reversible          │
  │  [x] Delegation  [~] Energy                              │
  │  ─────────────────────────────────────────────────       │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
  >> Start fundraise / Wait / Bootstrap instead
```

5. On decision to raise:
   - Log in DECISIONS.md
   - Route to INVESTOR:OS: "Open INVESTOR:OS and run `/investor:start-raise`"
   - Update PRIORITIES.md — fundraising should be priority #1 or #2
   - Update ROADMAP.md with fundraise timeline
6. On decision to wait: set a review date and runway trigger
7. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> If raising: /investor:start-raise in INVESTOR:OS
  >> If waiting: /founder:metrics to track triggers

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
