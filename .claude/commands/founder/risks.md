Risk register — identify, assess, and track what could go wrong.

Display:
```
<< FOUNDER:OS // RISKS >>
```

Follow these steps:

1. Read existing risks from ROADMAP.md and DECISIONS.md
2. Pull risk indicators from connected OS frameworks:
   - **FINANCE:OS** → runway declining, burn increasing, revenue flat
   - **GTM:OS** → pipeline shrinking, reply rates dropping, campaigns failing
   - **HR:OS** → key person risk, hiring stalled, morale issues
   - **INVESTOR:OS** → fundraise timeline slipping, investor ghosting
   - **COMMUNITY:OS** → engagement dropping, churn spiking
3. For each risk, assess:
   - **Likelihood:** low / medium / high
   - **Impact:** low / medium / high / critical
   - **Category:** financial, market, team, technical, legal, competitive
   - **Mitigation:** what can be done to reduce likelihood or impact
   - **Owner:** who is responsible for monitoring
   - **Trigger:** what signal tells you this risk is materializing
4. Display the risk register:

```
  ┌─ RISK REGISTER ─────────────────────────────────────────┐
  │                                                          │
  │  CRITICAL                                                │
  │  ! {risk} — Likelihood: high  Impact: critical           │
  │    Mitigation: {plan}  Owner: {name}                     │
  │                                                          │
  │  HIGH                                                    │
  │  ! {risk} — Likelihood: medium  Impact: high             │
  │    Mitigation: {plan}  Owner: {name}                     │
  │                                                          │
  │  MEDIUM                                                  │
  │  - {risk} — Likelihood: medium  Impact: medium           │
  │    Mitigation: {plan}  Owner: {name}                     │
  │                                                          │
  │  LOW                                                     │
  │  - {risk} — Likelihood: low  Impact: low                 │
  │    Mitigation: {plan}                                    │
  │                                                          │
  │  Total risks: {n}  Critical: {n}  High: {n}             │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

5. Ask if there are new risks to add or existing risks to update
6. For any critical or high risks with triggered signals, escalate immediately
7. Update ROADMAP.md with the risk register
8. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Risk register updated.
  {n} critical · {n} high · {n} medium · {n} low

  >> Next: /founder:decide · /founder:priorities

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
