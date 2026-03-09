Structured decision framework. Load `.claude/founderos/references/decision-frameworks.md` before running.

Display:
```
<< FOUNDER:OS // DECIDE >>
```

Follow these steps:

1. Ask: "What decision needs to be made?" — get a clear statement of the decision
2. Classify the decision:
   - **Type 1 (irreversible):** one-way door. Hard to undo. Examples: firing a key person, signing a lease, accepting investment terms, public pivot announcement
   - **Type 2 (reversible):** two-way door. Easy to undo. Examples: campaign strategy, pricing experiment, vendor switch, process change
3. If **Type 2:** Apply the 70% rule
   - Ask: "Do you have at least 70% confidence in a direction?"
   - If yes: decide now, log it, set a review date, move on
   - If no: identify the 1-2 missing data points, get them, then decide
   - Do not over-analyze Type 2 decisions — speed matters more than perfection
4. If **Type 1:** Run the full framework
   a. Pull relevant data from connected OS frameworks
   b. List all options (minimum 2, ideally 3)
   c. For each option, evaluate:
      - Pros and cons
      - OKR impact (which key result, by how much)
      - Financial impact (pull from FINANCE:OS if relevant)
      - Team impact (pull from HR:OS if relevant)
      - Risk level
   d. Score each option against the six decision gates:
      ```
      ── DECISION GATES ──────────────────────────────────
      [x] Vision       [x] OKR impact    [x] Data backed
      [x] Reversible   [x] Delegation    [x] Energy
      ─────────────────────────────────────────────────
      ```
   e. Ask: "Who else should weigh in on this?" — check NETWORK.md for advisors
   f. Present recommendation with rationale
5. Present the decision for approval:

```
  ┌─ DECISION ──────────────────────────────────────┐
  │                                                  │
  │  "{decision statement}"                          │
  │                                                  │
  │  Type:           {1/2}                           │
  │  Recommendation: {option}                        │
  │  OKR impact:     {which KR, expected impact}     │
  │  Risk:           {low/medium/high}               │
  │  Review date:    {date}                          │
  │                                                  │
  └──────────────────────────────────────────────────┘
  >> Approve / Reject / Defer / Need more data
```

6. On approval: log the decision in DECISIONS.md with full context, rationale, gates passed, and review date
7. If the decision routes work to another OS framework, create a delegation entry in DELEGATION.md
8. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Decision logged: D-{NNN}
  Review date: {date}

  >> Next: /founder:delegate · /founder:priorities

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
