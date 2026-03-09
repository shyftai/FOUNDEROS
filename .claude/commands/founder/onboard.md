Set up a new founder workspace. Run the full onboarding flow.

<< FOUNDER:OS // ONBOARDING >>

Follow these steps:

1. Ask the founder's role: Founder / CEO / Co-founder / COO
2. Ask company basics: name, stage (idea / pre-seed / seed / series-a / series-b / growth), team size
3. Ask execution mode preference: interactive (default, confirms decisions) or auto (auto-approves non-critical items)
4. Detect connected OS frameworks by checking which directories exist at /c/Antigravity/:
   - GTMOS → GTM:OS
   - CONTENTOS → CONTENT:OS
   - FINANCEOS → FINANCE:OS
   - HROS → HR:OS
   - INVESTOROS → INVESTOR:OS
   - COMMUNITYOS → COMMUNITY:OS
   Display which frameworks are detected with [x] / [ ]
5. Ask for the company vision and mission — write it as a future state
6. Ask for the north star metric — the one number that matters most
7. Ask for current top 3 priorities — what the founder is focused on right now
8. Ask for this quarter's OKRs — 2-3 objectives with 2-3 key results each
9. Ask about board composition — do they have a board? Who is on it?
10. Ask about key advisors and mentors
11. Create the workspace by copying _template/ to a new directory under workspaces/
12. Fill in workspace.config.md, VISION.md, OKRS.md, PRIORITIES.md, BOARD.md, and NETWORK.md with the gathered information
13. Display the workspace summary:

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

14. Suggest next steps:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> Next: /founder:today {workspace}
     Also: /founder:energy to set up your schedule
     Also: /founder:dashboard for full overview

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Group questions logically — do not ask all at once. Ask 2-3 questions per block, build on previous answers.
