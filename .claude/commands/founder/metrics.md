North star metric plus key metrics across all connected OS frameworks.

Display:
```
<< FOUNDER:OS // METRICS >>
```

Follow these steps:

1. Read workspace.config.md for the north star metric
2. Pull metrics from all connected OS frameworks
3. Display the north star prominently:

```
  ┌─ NORTH STAR ────────────────────────────────────┐
  │                                                  │
  │  {Metric name}                                   │
  │  Current: {value}                                │
  │  Target:  {value} by {date}                      │
  │  Trend:   {up/down/flat} ({%} change)            │
  │  ████████████░░░░  {progress}%                   │
  │                                                  │
  └──────────────────────────────────────────────────┘
```

4. Display domain metrics:

```
  ┌─ GTM METRICS ───────────────────────────────────┐
  │  Pipeline value:    ${amount}  ({trend})         │
  │  Weighted pipeline: ${amount}                    │
  │  Win rate:          {%}                          │
  │  Avg deal size:     ${amount}                    │
  │  Sales cycle:       {days} days                  │
  │  Reply rate:        {%}                          │
  │  Cost per meeting:  ${amount}                    │
  └──────────────────────────────────────────────────┘

  ┌─ FINANCIAL METRICS ─────────────────────────────┐
  │  MRR:              ${amount}  ({trend}% MoM)     │
  │  ARR:              ${amount}                     │
  │  Burn rate:        ${amount}/mo                  │
  │  Runway:           {months} months               │
  │  Gross margin:     {%}                           │
  │  LTV:CAC:          {ratio}                       │
  └──────────────────────────────────────────────────┘

  ┌─ TEAM METRICS ──────────────────────────────────┐
  │  Team size:        {n}                           │
  │  Open roles:       {n}                           │
  │  Time to hire:     {days} avg                    │
  │  Retention:        {%}                           │
  │  eNPS:             {score}                       │
  └──────────────────────────────────────────────────┘

  ┌─ GROWTH METRICS ────────────────────────────────┐
  │  Community members: {n} ({trend}% MoM)           │
  │  Engagement rate:   {%}                          │
  │  Content reach:     {n} ({trend}% MoM)           │
  │  Website traffic:   {n} ({trend}% MoM)           │
  └──────────────────────────────────────────────────┘
```

5. Flag any metrics that are concerning:
   - Runway below 6 months: `!!`
   - North star declining: `!!`
   - Burn increasing while revenue flat: `!!`
   - Key metric below benchmark (from BENCHMARKS.md): `!!`
6. Show metric trends over the last 4 weeks/months
7. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> Next: /founder:dashboard · /founder:review · /founder:report

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
