Manage the top 3 priorities. If everything is a priority, nothing is.

Display:
```
<< FOUNDER:OS // PRIORITIES >>
```

Follow these steps:

1. Read current PRIORITIES.md
2. Display current top 3 priorities with status:

```
  ┌─ CURRENT PRIORITIES ────────────────────────────┐
  │                                                  │
  │  1. {title}                                      │
  │     OKR: {link}  Status: {active/blocked}        │
  │     Owner: {name}  Due: {date}                   │
  │     Next action: {action}                        │
  │                                                  │
  │  2. {title}                                      │
  │     OKR: {link}  Status: {active/blocked}        │
  │     Owner: {name}  Due: {date}                   │
  │     Next action: {action}                        │
  │                                                  │
  │  3. {title}                                      │
  │     OKR: {link}  Status: {active/blocked}        │
  │     Owner: {name}  Due: {date}                   │
  │     Next action: {action}                        │
  │                                                  │
  └──────────────────────────────────────────────────┘
```

3. Show parked items from PRIORITIES.md
4. Ask what change is needed:
   - **Update status** — mark a priority as complete, blocked, or active
   - **Swap** — replace a priority (move current to parked, bring new one in)
   - **Reorder** — change the ranking of existing priorities
   - **Add to parked** — add something to the parked list for later
5. For any new priority, validate:
   - Which OKR does it serve? (If none, challenge whether it's truly a priority)
   - Who owns it?
   - What's the due date?
   - What's the very next action?
   - Should it be delegated?
6. Enforce the 3-priority maximum — if adding a 4th, one must be parked or completed
7. Update PRIORITIES.md
8. Log any priority changes in the change log
9. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Priorities updated.
  {n} active · {n} parked · {n} completed

  >> Next: /founder:delegate · /founder:today

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
