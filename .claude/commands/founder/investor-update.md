Generate an investor update from all connected OS framework data. HARD GATE — always requires explicit approval.

Display:
```
<< FOUNDER:OS // INVESTOR UPDATE >>
```

Follow these steps:

1. Ask: "Which period is this update for?" (e.g., January 2024, Q1 2024)
2. Ask: "Who is the audience?" (all investors, specific investor, prospective investor)
3. Pull data from all connected OS frameworks:
   - **GTM:OS** → revenue, pipeline, key wins, conversion metrics
   - **FINANCE:OS** → cash position, runway, burn rate, revenue growth
   - **HR:OS** → team growth, key hires
   - **INVESTOR:OS** → fundraising status (if active)
   - **CONTENT:OS** → press mentions, thought leadership wins
   - **COMMUNITY:OS** → community growth metrics
4. Pull OKR progress from OKRS.md
5. Draft the investor update — concise, data-first, no fluff:

   **TL;DR** (2-3 sentences — the whole update in a nutshell)

   **Key Metrics**
   | Metric | Value | MoM change |
   |--------|-------|-----------|
   | MRR/Revenue | | |
   | Cash/Runway | | |
   | Team size | | |
   | North star | | |
   | Pipeline | | |

   **Highlights** (3-5 bullets of good news)

   **Challenges** (1-2 bullets — be honest)

   **Asks** (specific, actionable)
   - Intros, advice, referrals — be precise

   **What's Next** (2-3 bullets for upcoming period)

6. Display with hard gate:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  INVESTOR UPDATE — {Period}                                  ┃
┃  HARD GATE: Requires explicit approval before sending        ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                                                              ┃
┃  {Full formatted update}                                     ┃
┃                                                              ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
  >> Approve / Edit / Reject
```

7. This is a HARD GATE — never auto-approve, even in auto mode
8. On approval: save to the workspace under investor-updates/{period}-investor-update.md
9. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Investor update saved.
  Next update due: {date based on cadence in workspace.config.md}

  >> Next: /founder:board-update · /founder:fundraise

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
