Full company overview across all connected OS frameworks. More detailed than /founder:today.

Display:
```
<< FOUNDER:OS // DASHBOARD >>
```

Follow these steps:

1. Pull comprehensive data from each connected OS framework
2. Display the full company dashboard:

```
  ┌─ COMPANY DASHBOARD ─────────────────────────────────────┐
  │                                                          │
  │  {Company Name}  ·  {Stage}  ·  {Team size} people      │
  │  North star: {metric} = {current value} (target: {tgt})  │
  │                                                          │
  ├─ REVENUE & PIPELINE (GTM:OS) ───────────────────────────┤
  │  Pipeline value:     ${amount} ({n} deals)               │
  │  Weighted pipeline:  ${amount}                           │
  │  Active campaigns:   {n}                                 │
  │  Reply rate:         {%}  |  Meeting rate: {%}           │
  │  Meetings this week: {n}  |  Meetings this month: {n}   │
  │  Cost per meeting:   ${amount}                           │
  │                                                          │
  ├─ FINANCIAL HEALTH (FINANCE:OS) ─────────────────────────┤
  │  Cash position:      ${amount}                           │
  │  Monthly burn:       ${amount}                           │
  │  Runway:             {months} months                     │
  │  Revenue (MRR):      ${amount} ({trend}% MoM)           │
  │  Overdue invoices:   {n} (${total})                     │
  │                                                          │
  ├─ TEAM (HR:OS) ──────────────────────────────────────────┤
  │  Team size:          {n} ({n} FT, {n} contractors)       │
  │  Open roles:         {n}                                 │
  │  Pending offers:     {n}                                 │
  │  Avg time to hire:   {n} days                            │
  │  Reviews due:        {n}                                 │
  │                                                          │
  ├─ FUNDRAISING (INVESTOR:OS) ─────────────────────────────┤
  │  Stage:              {current fundraise or "not raising"} │
  │  Pipeline:           {n} investors ({n} active convos)   │
  │  Follow-ups due:     {n}                                 │
  │  Last update sent:   {date}                              │
  │                                                          │
  ├─ CONTENT (CONTENT:OS) ──────────────────────────────────┤
  │  Published this week: {n}                                │
  │  Scheduled:          {n} upcoming                        │
  │  Top performing:     {title} ({views} views)             │
  │  Content pipeline:   {n} in draft                        │
  │                                                          │
  ├─ COMMUNITY (COMMUNITY:OS) ──────────────────────────────┤
  │  Total members:      {n} ({trend} this month)            │
  │  Engagement rate:    {%}                                 │
  │  Events this week:   {n}                                 │
  │  Churn rate:         {%}                                 │
  │  Revenue (if paid):  ${MRR}                              │
  │                                                          │
  ├─ CUSTOMER SUCCESS (CS:OS) ─────────────────────────────┤
  │  NRR:                {%} ({trend})                       │
  │  Customers:          {n} total  |  {n} at risk           │
  │  ARR at risk:        ${amount}                           │
  │  Renewals this month: {n} (${amount})                    │
  │  NPS:                {score} ({trend})                   │
  │  Expansion pipeline: ${amount} ({n} opportunities)       │
  │  Health: {n}% healthy  {n}% stable  {n}% at-risk        │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

3. Show OKR summary with progress bars:

```
  ┌─ OKR PROGRESS ──────────────────────────────────────────┐
  │                                                          │
  │  O1: {objective}                                         │
  │      KR1: {result}  ████████░░  80%  [on track]         │
  │      KR2: {result}  ██████░░░░  60%  [on track]         │
  │      KR3: {result}  ███░░░░░░░  30%  [at risk]          │
  │                                                          │
  │  O2: {objective}                                         │
  │      KR1: {result}  █████████░  90%  [on track]         │
  │      KR2: {result}  ████░░░░░░  40%  [behind]           │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

4. Show priorities and their status
5. Show pending decisions with urgency
6. Show recent learnings (last 3 from LEARNINGS.md)
7. Flag any items that need founder attention with `!!`
8. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> What needs your attention?
     /founder:decide · /founder:priorities · /founder:weekly

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

For any framework that is not connected or has no data, show the section with "Not connected" or "No data available" instead of leaving it blank.
