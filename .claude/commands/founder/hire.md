Hiring decision framework. This command helps the founder decide WHAT to hire and WHY — then routes execution to HR:OS.

Display:
```
<< FOUNDER:OS // HIRE >>
```

Follow these steps:

1. Ask: "What role are you considering hiring for?"
2. Run the hiring decision framework:
   a. **Need validation:** Is this hire necessary right now?
      - Which OKR does this role serve?
      - What happens if you don't hire for 3 more months?
      - Could this be solved with a contractor, tool, or redistribution?
   b. **Financial check:** Can you afford this hire?
      - Pull runway from FINANCE:OS
      - Calculate impact on burn rate (salary + 20-30% overhead)
      - How many months does this shorten runway?
   c. **Priority check:** Is this the most important hire right now?
      - Compare against other open roles (pull from HR:OS)
      - Stack rank all hiring needs against OKR impact
   d. **Profile definition:**
      - What does this person need to do in the first 90 days?
      - What's the must-have vs nice-to-have skill split?
      - What level (junior/mid/senior/lead)?
      - Remote/hybrid/onsite?
3. This is a **Type 1 decision** for senior hires, Type 2 for junior hires
4. Run decision quality gates
5. Display:

```
  ┌─ HIRING DECISION ───────────────────────────────┐
  │                                                  │
  │  Role:        {title}                            │
  │  OKR link:    {which key result}                 │
  │  Type:        {1/2}                              │
  │                                                  │
  │  Financial impact:                               │
  │    Salary range:    ${min}-${max}                 │
  │    Burn increase:   ${amount}/mo                  │
  │    Runway impact:   -{n} months                   │
  │                                                  │
  │  Priority rank:     #{n} of {total open roles}   │
  │                                                  │
  │  90-day outcomes:                                │
  │  1. {what they should achieve}                   │
  │  2. {what they should achieve}                   │
  │  3. {what they should achieve}                   │
  │                                                  │
  │  ── DECISION GATES ────────────────────────────  │
  │  [x] Vision  [x] OKR  [x] Data  [x] Energy     │
  │  ─────────────────────────────────────────────   │
  │                                                  │
  └──────────────────────────────────────────────────┘
  >> Approve hire / Defer / Contract instead
```

6. On approval:
   - Log decision in DECISIONS.md
   - Create delegation entry routing to HR:OS
   - Suggest: "Open HR:OS and run `/hr:open-role {title}`"
7. On deferral: log the decision with review date
8. End with route to HR:OS for execution
