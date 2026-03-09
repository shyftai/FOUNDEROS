Daily cockpit — the founder's morning briefing. Pull data from ALL connected OS frameworks.

Display:
```
<< FOUNDER:OS // TODAY >>
```

Follow these steps:

1. Display the date and any calendar events from ENERGY.md
2. Check all connected OS frameworks by scanning their workspace directories for key files:
   - **GTM:OS** → read workspace.config.md, PIPELINE.md for pipeline value; scan active campaigns for reply rate, meetings booked today
   - **CONTENT:OS** → read CALENDAR.md for content due today, publishing schedule
   - **FINANCE:OS** → read DASHBOARD.md or key files for runway, cash position, burn rate, overdue invoices
   - **HR:OS** → read HIRING.md for open roles, pending offers; REVIEWS.md for reviews due
   - **INVESTOR:OS** → read PIPELINE.md for investor pipeline status, follow-ups due, meetings scheduled
   - **COMMUNITY:OS** → read METRICS.md for engagement rate, new members; EVENTS.md for events today
3. Display the company pulse dashboard:

```
  ┌─ COMPANY PULSE ──────────────────────────────────┐
  │                                                    │
  │  GTM:OS        Pipeline: ${value}  Meetings: {n}   │
  │                Reply rate: {%}  Active campaigns: {n}
  │  FINANCE:OS    Runway: {months}  Burn: ${amount}/mo │
  │                Cash: ${position}  Overdue: {n}      │
  │  HR:OS         Open roles: {n}  Offers pending: {n} │
  │                Reviews due: {n}                     │
  │  INVESTOR:OS   Pipeline: {n}  Follow-ups due: {n}  │
  │                Next meeting: {date}                 │
  │  CONTENT:OS    Due today: {n}  Weekly cadence: {n}  │
  │  COMMUNITY:OS  Members: {n}  Engagement: {%}       │
  │                Events today: {n}                    │
  │                                                    │
  └────────────────────────────────────────────────────┘
```

4. Show OKR progress from OKRS.md — flag any at-risk or behind key results with `!!`
5. Show today's top 3 priorities from PRIORITIES.md with their status
6. Show pending decisions from DECISIONS.md with deadlines
7. Show energy/calendar blocks from ENERGY.md — deep work time, meetings scheduled
8. Flag urgent items across all frameworks:
   - Cash runway below 6 months
   - OKR key result more than 20% behind
   - Overdue investor follow-ups
   - Board meeting within 7 days
   - Open roles with no candidates for 30+ days
   - Stalled deals in pipeline
9. Suggest top 3 actions for today based on urgency and OKR impact:

```
  Top 3 actions for today:
  1. {Action — which OS, why it matters, type of work}
  2. {Action}
  3. {Action}
```

10. End with next action prompt:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> What would you like to focus on?
     /founder:decide · /founder:delegate · /founder:dashboard

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

If a connected OS framework has no workspace data yet, show `{Framework}: No data — run its onboard command` instead of empty metrics.
