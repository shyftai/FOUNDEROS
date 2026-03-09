Company performance report. Generates a structured report from all connected OS data.

Load `.claude/founderos/references/report-template.md` before running.

Display:
```
<< FOUNDER:OS // REPORT >>
```

Follow these steps:

1. Ask: "What type of report? Company performance / department review / custom"
2. Ask: "What period? Weekly / monthly / quarterly / custom range"
3. Ask: "Who is the audience? Internal team / board / investors / self"
4. Pull data from all connected OS frameworks for the period
5. Generate the report with sections adapted to audience:

**For internal team:**
- North star metric and trend
- Department highlights from each OS
- OKR progress
- Wins and misses (be candid)
- Action items for next period

**For board:** (use /founder:board-update format)

**For investors:** (use /founder:investor-update format)

**For self (founder reflection):**
- Honest assessment across all domains
- Decision quality review
- Energy and sustainability check
- Strategic position assessment

6. Display the report:

```
  ┌─ COMPANY REPORT — {Period} ─────────────────────────────┐
  │                                                          │
  │  {Full formatted report content}                         │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

7. If audience is board or investors: apply HARD GATE before sending
8. Save report to workspace under reports/{period}-{type}-report.md
9. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Report saved: reports/{filename}

  >> Next: /founder:review · /founder:debrief · /founder:board-update

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
