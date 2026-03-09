Generate a board update from all connected OS framework data. HARD GATE — always requires explicit approval.

Load `.claude/founderos/references/board-guide.md` before running.

Display:
```
<< FOUNDER:OS // BOARD UPDATE >>
```

Follow these steps:

1. Read BOARD.md for board composition and update format preferences
2. Ask: "Which period is this update for?" (e.g., Q1 2024, January 2024)
3. Pull data from all connected OS frameworks:
   - **GTM:OS** → revenue/pipeline, campaign performance, meetings booked, conversion rates, cost per acquisition
   - **FINANCE:OS** → cash position, burn rate, runway, revenue trend, budget vs actual, overdue AR
   - **HR:OS** → team changes (hires, departures), open roles, org updates, culture initiatives
   - **INVESTOR:OS** → fundraising status, investor conversations, cap table changes
   - **CONTENT:OS** → content performance, brand metrics, thought leadership progress
   - **COMMUNITY:OS** → community growth, engagement, events, revenue from community
4. Pull OKR progress from OKRS.md
5. Pull key decisions from DECISIONS.md for this period
6. Draft the board update in five sections:

   **Section 1: Highlights** (3-5 bullets)
   - Major wins and milestones this period

   **Section 2: Key Metrics** (table format)
   - Revenue, pipeline, burn, runway, team size, north star metric
   - Show last period vs this period vs target

   **Section 3: Challenges** (2-3 bullets)
   - What's not working and what you're doing about it
   - Be candid — boards respect honesty over spin

   **Section 4: Asks** (1-2 specific requests)
   - Introductions, advice, decisions requiring board input
   - Be specific: "Intro to [name] at [company]" not "help with partnerships"

   **Section 5: Next Period Outlook**
   - Top 3 priorities
   - Key hires planned
   - Expected milestones

7. Display the draft:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  BOARD UPDATE — {Period}                                     ┃
┃  HARD GATE: Requires explicit approval before sending        ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                                                              ┃
┃  {Full formatted update}                                     ┃
┃                                                              ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
  >> Approve / Edit / Reject
```

8. This is a HARD GATE — never auto-approve, even in auto mode
9. On approval: save to the workspace under board-updates/{period}-board-update.md
10. Log the communication in BOARD.md communication log
11. End with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Board update saved: board-updates/{period}-board-update.md
  Logged in BOARD.md

  >> Next: /founder:investor-update · /founder:review

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
