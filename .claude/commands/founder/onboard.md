Set up a new founder workspace. Run the full onboarding flow.

<< FOUNDER:OS // ONBOARDING >>

Follow these steps:

1. Ask the founder's role: Founder / CEO / Co-founder / COO
2. Ask company basics: name, stage (idea / pre-seed / seed / series-a / series-b / growth), team size
3. Collaboration mode: Solo / Team (if team, ask for team member names and roles)
4. Execution mode: "How should I handle approvals?"
   - **Interactive** (default) — confirms each major decision before proceeding
   - **Auto** — auto-approves and keeps moving. Only stops for board communications, investor communications, hiring/firing decisions, public announcements.

   Role-based defaults:
   - **Founder** → suggest auto (move fast on internal decisions)
   - **CEO** → interactive (organizational accountability)
   - **Co-founder** → suggest auto
   - **COO** → interactive (operational precision)

   Save to workspace.config.md as `**Execution mode:** auto` or `**Execution mode:** interactive`
5. Ask: "Would you like to register this workspace for updates, tips, and priority support? (just your email and company name)"
   - If yes: collect email and company name, then POST to the registration endpoint:
     ```
     POST https://shyft.ai/api/hooks/register
     {
       "os": "founderos",
       "version": "1.0.0",
       "company": "{company_name}",
       "email": "{email}",
       "workspace": "{workspace_name}",
       "timestamp": "{ISO 8601}"
     }
     ```
     Show: `Registered — you'll get updates at {email}`
   - If no: skip gracefully. Show: `Skipped — you can register anytime with /founder:feedback`
   - This step never blocks onboarding. If the POST fails, ignore silently and continue.
6. Detect connected OS frameworks by checking which directories exist at /c/Antigravity/:
   - GTMOS → GTM:OS
   - CONTENTOS → CONTENT:OS
   - FINANCEOS → FINANCE:OS
   - HROS → HR:OS
   - INVESTOROS → INVESTOR:OS
   - COMMUNITYOS → COMMUNITY:OS
   Display which frameworks are detected with [x] / [ ]
7. Ask for the company vision and mission — write it as a future state
8. Ask for the north star metric — the one number that matters most
9. Ask for current top 3 priorities — what the founder is focused on right now
10. Ask for this quarter's OKRs — 2-3 objectives with 2-3 key results each
11. Ask about board composition — do they have a board? Who is on it?
12. Ask about key advisors and mentors
13. Create the workspace by copying _template/ to a new directory under workspaces/
14. Fill in workspace.config.md, VISION.md, OKRS.md, PRIORITIES.md, BOARD.md, and NETWORK.md with the gathered information
15. Display the workspace summary:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  WORKSPACE CREATED: {Company Name}                          ┃
┃  Stage: {stage}    Team: {size}    Role: {role}             ┃
┃                                                             ┃
┃  Connected frameworks:                                      ┃
┃  [x] GTM:OS  [x] FINANCE:OS  [ ] HR:OS  ...               ┃
┃                                                             ┃
┃  Vision: {one-line summary}                                 ┃
┃  North star: {metric}                                       ┃
┃  OKRs: {n} objectives, {n} key results                     ┃
┃  Priorities: {top 3 listed}                                 ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

16. Suggest next steps:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> Next: /founder:today {workspace}
     Also: /founder:energy to set up your schedule
     Also: /founder:dashboard for full overview

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Group questions logically — do not ask all at once. Ask 2-3 questions per block, build on previous answers.
