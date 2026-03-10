# Video Scripts — Phase 2, Batch 1 (Deep Dives)

> Antigravity OS ecosystem by Shyft AI
> Format: Deep-dive screen recording, founder-narrated walkthrough in Claude Code
> Length: 5-10 minutes each
> Platform: YouTube (long-form)

---
---

## Script 1: "Build a Complete Outbound Campaign in 10 Minutes"

**Total runtime:** ~9 minutes
**OS:** GTM:OS

---

### TITLE CARD (0:00 - 0:05)

[SCREEN] Black background. Text fades in:

```
BUILD A COMPLETE OUTBOUND CAMPAIGN
IN 10 MINUTES

GTM:OS by Shyft AI
```

[TEXT OVERLAY] Small watermark bottom-right: "shyft.ai"

---

### HOOK (0:05 - 0:30)

[SCREEN] Split screen montage — left side: Notion board with 40+ cards, Outreach.io sequence editor, a Google Sheet with 2000 rows, Salesforce filter view, a Slack thread with 11 replies about copy feedback. Right side: a single terminal window, cursor blinking.

[VO] "Building an outbound campaign normally goes like this. Your SDR spends Monday morning building a list in Sales Navigator. Your copywriter drafts a sequence Tuesday. Marketing reviews it Wednesday. Someone loads it into the sending tool Thursday. And if you're lucky, emails go out Friday. That's a full week. Five people. Six tools."

[SCREEN] Left side fades to black. Terminal fills the screen.

[VO] "I'm going to do the whole thing right now. From zero to launch-ready. In one terminal."

---

### CONTEXT (0:30 - 1:00)

[SCREEN] Terminal. Clean. No windows open except Claude Code.

[VO] "What you're about to see is GTM:OS — an open-source go-to-market operating system that runs inside Claude Code. It handles ICP definition, list strategy, copy, validation, and launch checks. Everything lives in markdown files. Everything is version-controlled. And every step has quality gates so nothing ships that shouldn't."

[TEXT OVERLAY] Bottom-left: "GTM:OS v1.4.0 — open source — github.com/shyftai"

[VO] "Let's say we're a B2B SaaS company selling developer productivity tools. We need to reach engineering leaders at mid-market companies. Let's build the whole campaign."

---

### WALKTHROUGH — STEP 1: ONBOARD (1:00 - 2:30)

[SCREEN] Terminal. User types: `/gtm:onboard devtools-q1`

[VO] "First, we onboard. This creates the workspace and captures everything the system needs to write and target correctly."

[SCREEN] GTM:OS boot banner appears — bold orange ASCII art, version number, Shyft AI attribution. System status panel loads showing MCP servers and API key status.

[VO] "The system boots, checks which tools are connected — Apollo for prospecting, Instantly for sending, Attio for CRM — and starts the structured intake."

[SCREEN] Structured intake begins. Prompts appear one at a time:

```
Company name?          > DevForge
Product / service?     > Code review automation platform
Website?               > devforge.io
One-line value prop?   > Ship code 3x faster with AI-powered review
```

[VO] "Company basics first. Name, product, value prop. Nothing fancy — just the foundation everything else builds on."

[SCREEN] ICP section:

```
ICP DEFINITION
  Industry?            > SaaS, Fintech, DevTools
  Company size?        > 100-2000 employees
  Geography?           > US, UK, Germany
  Revenue range?       > $10M - $200M ARR
  Budget authority?    > VP Engineering, CTO, Head of Platform
  Buying signals?      > Hiring backend engineers, SOC2 compliance, Series B+
```

[VO] "Now the ICP. And this isn't a slide in a deck nobody reads. This becomes a scoreable filter. Every lead that comes in later gets scored against exactly these criteria."

[SCREEN] Persona builder:

```
PRIMARY PERSONA
  Title:               VP of Engineering
  Reports to:          CTO
  Cares about:         Developer velocity, code quality, retention
  Pain points:         PR bottleneck, slow review cycles, senior eng burnout
  Objections:          "We already use GitHub Copilot", "My team won't adopt another tool"
  Messaging angles:    Speed (3x), Quality (fewer bugs), Retention (less burnout)
```

[VO] "The persona section captures not just who they are, but what they object to and what messaging angles work. This feeds directly into the copy engine later."

[SCREEN] Tone of voice selector:

```
TONE OF VOICE
  [x] Direct, not aggressive
  [x] Technical, not jargon-heavy
  [x] Peer-to-peer, not salesy
  [ ] Formal
  [ ] Casual / humor
```

[VO] "Tone of voice locks in. Every email this system writes will follow these constraints. No drift. No 'Hey there!!!' when you told it to sound technical."

[SCREEN] Workspace created confirmation. Files listed:

```
Workspace created: /workspaces/devtools-q1/
  workspace.config.md
  ICP.md
  PERSONAS.md
  TOV.md
  RULES.md
  SUPPRESSION.md
  LEARNINGS.md
```

[VO] "Workspace created. Seven files. Everything the system needs is now structured, searchable, and locked in."

---

### WALKTHROUGH — STEP 2: RESEARCH (2:30 - 3:15)

[SCREEN] Types: `/gtm:research`

[VO] "Next — research. Before we write anything, we need to understand the landscape."

[SCREEN] Research output starts rendering:

```
MARKET LANDSCAPE
  TAM: ~4,200 companies matching ICP in US/UK/DE
  Active competitors: Codacy, CodeClimate, Graphite, LinearB
  Market signal: "AI code review" mentions up 340% YoY (Google Trends)

COMPETITOR POSITIONING
  Codacy        → Quality-first, enterprise play
  CodeClimate   → Metrics-heavy, engineering managers
  Graphite      → Speed-first, developer workflow
  LinearB       → Efficiency metrics, VP-level dashboards

SIGNAL ANGLES (recommended)
  1. Companies posting "slow PR reviews" on engineering blogs
  2. Job posts mentioning "code review process" improvements
  3. Companies with 50+ open PRs on public GitHub repos
  4. Recent SOC2 certification (compliance = process maturity)

DIFFERENTIATORS TO LEAD WITH
  - AI-native (not bolted on)
  - 3x speed claim with customer proof points
  - Developer-loved (not just manager-loved)
```

[VO] "Market sizing. Competitor positioning. And — this is the important part — signal angles. These are the triggers that tell us a company is actively feeling the pain we solve. We're not spray-and-praying. We're targeting companies where the timing is right."

---

### WALKTHROUGH — STEP 3: NEW CAMPAIGN (3:15 - 3:50)

[SCREEN] Types: `/gtm:new-campaign`

[VO] "Now we create the campaign shell."

[SCREEN] Campaign setup:

```
CAMPAIGN SETUP
  Campaign name?       > q1-eng-leaders-code-review
  Campaign type?       > cold-outbound (4-touch email)
  Channel?             > email
  Touches?             > 4
  Spacing?             > Day 1 / Day 3 / Day 7 / Day 14
  Sending tool?        > Instantly
  Daily send limit?    > 40 per sender
  Senders?             > 3 accounts
```

[VO] "Four-touch email sequence. Spaced across two weeks. Three sender accounts at 40 per day — that's 120 sends daily, well within safe deliverability limits. The system knows these thresholds. It won't let you set 500 a day and torch your domain."

[SCREEN] Campaign file saved confirmation.

---

### WALKTHROUGH — STEP 4: LIST BRIEF (3:50 - 4:30)

[SCREEN] Types: `/gtm:list-brief`

[VO] "Before we build the list, we write the list brief. This is the targeting document — what goes in, what stays out."

[SCREEN] List brief output:

```
LIST BRIEF — q1-eng-leaders-code-review
  Target count:        500 leads
  Source:              Apollo

  INCLUDE
    Title: VP Engineering, CTO, Head of Platform, Director of Engineering
    Company size: 100-2000
    Industry: SaaS, Fintech, DevTools
    Location: US, UK, Germany
    Funding: Series B+

  EXCLUDE
    Current customers (from SUPPRESSION.md)
    Companies < 50 employees
    Competitors: Codacy, CodeClimate, Graphite, LinearB
    Previous bounces (from SUPPRESSION.md)

  ENRICHMENT
    Required: verified email, LinkedIn URL, company tech stack
    Nice-to-have: recent funding round, open roles, GitHub activity
```

[VO] "Five hundred leads. Tight filters. And look at the exclude section — it automatically pulls in our suppression list. Current customers, previous bounces, competitors. These are the details that get missed when a human does this manually and somebody's CEO gets a cold email from their own vendor."

---

### WALKTHROUGH — STEP 5: WRITE SEQUENCE (4:30 - 6:30)

[SCREEN] Types: `/gtm:write`

[VO] "Now the fun part. Writing the sequence."

[SCREEN] System shows it loading workspace context:

```
Loading context...
  ICP.md .............. loaded
  PERSONAS.md ......... loaded
  TOV.md .............. loaded
  RULES.md ............ loaded
  LEARNINGS.md ........ loaded (0 learnings — first campaign)
  campaign-brief.md ... loaded
```

[VO] "Watch this. It loads every piece of context we've built — ICP, persona, tone of voice, workspace rules, and the learnings file. That learnings file is empty right now because this is our first campaign. But after we run this, debrief, and improve? The next campaign gets smarter."

[SCREEN] Touch 1 appears:

```
TOUCH 1 — Initial
Subject: {{company}} PR reviews
---
{{first_name}},

Talked to three VPs of Engineering last month who all said the same thing:
PR reviews are where velocity goes to die.

{{company}} has {{open_roles_engineering}} open engineering roles right now.
More engineers, more PRs, slower reviews — unless the process changes.

DevForge cuts review cycles by 3x using AI that actually understands
your codebase. Not generic suggestions — context-aware analysis.

Worth a 15-minute look?

— {{sender_name}}
```

[VO] "Touch one. Short. Pain-focused. Notice the personalization variables — first name, company name, and open engineering roles. That's not a mail merge gimmick. It's a signal that says 'I know you're hiring, and that's going to make your PR bottleneck worse.' That's relevance."

[SCREEN] Touches 2, 3, and 4 appear in sequence, each with different angles:

```
TOUCH 2 — Value proof (Day 3)
Subject: re: {{company}} PR reviews
---
Quick follow-up — here's what changed for one team like yours:

Before DevForge: 4.2 hours average PR review time
After: 1.1 hours. First week.

Not asking for a meeting. Just curious if review speed
is something {{company}} is actively trying to fix right now.

---

TOUCH 3 — Social proof (Day 7)
Subject: {{competitor_customer}} switched last quarter
---
{{first_name}} — {{competitor_customer}} moved off their old review
process in Q3 and shipped their SOC2 audit 6 weeks early.

Their VP Eng said the AI reviewer caught 40% of the issues their
senior devs used to flag manually.

Different situation, but if code quality and speed are on your
radar, might be relevant.

---

TOUCH 4 — Breakup (Day 14)
Subject: closing the loop
---
{{first_name}} — totally fine if this isn't a priority right now.

Deleting this thread from my follow-up list. If code review speed
comes up in a planning cycle, here's where to find us: devforge.io

No hard feelings either way.
```

[VO] "Touch two leads with proof — specific numbers, not vague claims. Touch three is social proof — a named customer, a concrete result. Touch four is the breakup. No guilt trip. No 'just bumping this up.' Clean exit. Respectful. And every single one of these follows the tone of voice we set in onboarding — direct, technical, peer-to-peer."

---

### WALKTHROUGH — STEP 6: VALIDATE (6:30 - 7:20)

[SCREEN] Types: `/gtm:validate-copy`

[VO] "Before anything ships, it has to pass validation. Five automated checks."

[SCREEN] Validation runs:

```
COPY VALIDATION — q1-eng-leaders-code-review

  1. BRIEF COMPLIANCE                              PASS
     All touches match campaign brief and ICP targeting.

  2. TOV COMPLIANCE                                 PASS
     Tone matches workspace TOV settings.
     No salesy language detected. No exclamation marks.
     Reading level: Grade 8 (target: 7-9). OK.

  3. SPAM & DELIVERABILITY                          PASS
     No spam trigger words found.
     Link count: 1 per touch (max 1). OK.
     No image attachments. OK.
     CAN-SPAM compliant.

  4. PERSONALIZATION CHECK                          PASS
     All merge fields map to available data columns.
     No invented fields. No hardcoded company names.
     Fallback values defined for optional fields.

  5. SUPPRESSION CHECK                              PASS
     Cross-referenced against SUPPRESSION.md.
     0 conflicts found.

  OVERALL: 5/5 PASSED
  Copy is approved for launch.
```

[VO] "Five checks. Brief compliance — does the copy match what we briefed? Tone compliance — is it actually written the way we said? Spam and deliverability — any trigger words, too many links, anything that'll land in spam? Personalization — are all the merge fields real, or did someone invent a variable that doesn't exist in the data? And suppression — are we about to email someone we shouldn't? Five out of five. Green across the board."

---

### WALKTHROUGH — STEP 7: SHIP (7:20 - 8:15)

[SCREEN] Types: `/gtm:ship`

[VO] "Last step. Ship. And this is where the hard gate lives."

[SCREEN] Launch check dashboard appears:

```
LAUNCH CHECK — q1-eng-leaders-code-review
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  PRE-FLIGHT
  [x] Campaign brief complete
  [x] List brief approved
  [x] Copy validated (5/5 checks passed)
  [x] Suppression list current (updated today)
  [x] Sending calendar checked — no holidays this week
  [x] Domain health: all 3 senders warmed, DKIM/SPF/DMARC pass
  [x] Daily volume within safe limits (40/sender)

  COST CHECK
  [x] Apollo credits: 500 leads x $0.03 = $15.00
  [x] Instantly sends: 2,000 emails x $0.002 = $4.00
  [x] Total campaign cost: $19.00

  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  HARD GATE — HUMAN APPROVAL REQUIRED

  This campaign will send 2,000 emails to 500 people
  over 14 days from 3 sender accounts.

  >> Type APPROVED to launch, or HOLD to pause.
```

[VO] "Everything checked. List ready, copy validated, suppression current, domains healthy, no holiday conflicts, costs calculated. And then — the hard gate. This is the one thing the system will never skip. A human has to type APPROVED. Not a checkbox. Not a 'looks good.' You type the word. Because sending email is irreversible, and this system respects that."

[SCREEN] User types: `APPROVED`

```
  APPROVED at 2026-03-10 09:47 UTC
  Campaign q1-eng-leaders-code-review is LIVE.
  Logged to COSTS.md: $19.00
  First sends begin: tomorrow 8:00 AM recipient local time
```

[VO] "Approved. Logged. Launching tomorrow morning in recipient local time. Cost tracked automatically."

---

### RESULTS RECAP (8:15 - 8:45)

[SCREEN] Split view — left shows the terminal with the full workflow visible (scrolled), right shows a file tree of the workspace:

```
/workspaces/devtools-q1/
  workspace.config.md
  ICP.md
  PERSONAS.md
  TOV.md
  RULES.md
  SUPPRESSION.md
  LEARNINGS.md
  campaigns/
    q1-eng-leaders-code-review/
      campaign-brief.md
      list-brief.md
      sequence.md
      validation-report.md
      launch-log.md
  research/
    market-landscape.md
  COSTS.md
```

[VO] "So what did we just build? A fully researched, targeted, four-touch outbound campaign. ICP defined. Market researched. List strategy locked. Copy written, validated against five quality checks, and approved through a hard gate. Every artifact saved as a markdown file. Version-controlled. Auditable. Improvable. This would normally take a team two to three days. We did it in ten minutes. From one terminal."

---

### CTA (8:45 - 9:00)

[SCREEN] Terminal. Text appears:

```
GTM:OS — open source
github.com/shyftai

Clone it. Run /gtm:onboard. Build your first campaign.
```

[TEXT OVERLAY] "Subscribe for more deep dives. Next: CS:OS end-to-end."

[VO] "GTM:OS is free and open source. Link in the description. Clone it, run /gtm:onboard, and build your first campaign in ten minutes. Subscribe — next video, I'm showing the full customer success lifecycle from deal handoff to renewal. See you there."

---
---

## Script 2: "Customer Success OS: From Handoff to Renewal"

**Total runtime:** ~8 minutes
**OS:** CS:OS (with GTM:OS handoff)

---

### TITLE CARD (0:00 - 0:05)

[SCREEN] Black background. Text fades in:

```
CUSTOMER SUCCESS OS
FROM HANDOFF TO RENEWAL

CS:OS by Shyft AI
```

---

### HOOK (0:05 - 0:35)

[SCREEN] A Slack channel scrolling with messages: "Did anyone loop in CS on the Acme deal?" / "What did we promise them in the sales cycle?" / "Who owns this account?" / "They're asking about the feature we mentioned in the demo — did we actually commit to that?"

[VO] "This is what the handoff from sales to customer success looks like at most companies. A Slack thread. A half-filled CRM record. And a customer who was promised the moon by a sales rep who's already moved on to the next deal."

[SCREEN] Cut to clean terminal.

[VO] "Sixty-seven percent of churn starts in the first ninety days. Not because the product is bad — because the handoff is. I'm going to show you the entire customer lifecycle, from the moment a deal closes to the moment it renews, in one system."

---

### CONTEXT (0:35 - 1:00)

[SCREEN] Terminal with CS:OS about to boot.

[VO] "CS:OS is a customer success operating system that runs in Claude Code. It connects to GTM:OS for deal handoffs, tracks health across five dimensions, runs playbooks when accounts go at-risk, and has hard gates on anything customer-facing. Let's walk through a full lifecycle."

[TEXT OVERLAY] Bottom-left: "CS:OS v1.0.0 — open source — github.com/shyftai"

---

### WALKTHROUGH — STEP 1: HANDOFF (1:00 - 1:50)

[SCREEN] Types: `/cs:handoff`

[VO] "The lifecycle starts here. A deal just closed in GTM:OS and we're receiving the handoff."

[SCREEN] CS:OS boot banner — blue ASCII art, version number, Shyft AI attribution. System status loads.

[SCREEN] Handoff intake begins:

```
DEAL HANDOFF — Receiving from GTM:OS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Account:          Meridian Technologies
  Deal value:       $84,000 ARR
  Contract:         12-month annual
  Close date:       2026-03-08
  Sales owner:      Jake Morrison

  STAKEHOLDER MAP (from sales cycle)
  Decision maker:   Sarah Chen, VP Engineering
  Champion:         Marcus Webb, Director of Platform
  Technical lead:   Priya Sharma, Staff Engineer
  Exec sponsor:     David Liu, CTO (light involvement)

  PROMISES TRACKED
  1. Custom SSO integration — committed, timeline Q2
  2. Dedicated onboarding engineer — first 30 days
  3. Quarterly business reviews — committed
  4. API rate limit increase — "we'll look into it" (soft)

  RED FLAGS FROM SALES CYCLE
  - Competitive eval with LinearB (close call)
  - Long procurement cycle (4 months)
  - CTO only attended 1 of 5 meetings

  AUTO-CREATED
  [x] Customer record: /customers/meridian/customer.md
  [x] Stakeholder map saved
  [x] Promise tracker initialized
  [x] Onboarding milestone template applied
  [x] First check-in scheduled: Day 14
```

[VO] "Look at what just happened. The system pulled the full deal context — who was involved, what was promised, and what the red flags were. That promise tracker is critical. 'Custom SSO — committed.' 'API rate limit — soft.' Those are different categories. One is a contract obligation. The other is a 'nice to have' the sales rep mentioned in passing. CS:OS tracks both, but treats them differently. And notice the auto-created files. Customer record, stakeholder map, promise tracker, milestone template. The CS team can start working immediately."

---

### WALKTHROUGH — STEP 2: KICKOFF (1:50 - 2:40)

[SCREEN] Types: `/cs:kickoff meridian`

[VO] "Now we build the kickoff plan."

[SCREEN] Kickoff plan generates:

```
KICKOFF PLAN — Meridian Technologies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  AGENDA (60 minutes)
  1. Introductions & roles (5 min)
  2. Recap success criteria from sales cycle (10 min)
  3. Onboarding timeline walkthrough (15 min)
  4. Technical requirements & integrations (15 min)
  5. Communication cadence & escalation paths (10 min)
  6. Q&A (5 min)

  SUCCESS CRITERIA (aligned with sales cycle)
  - Reduce PR review time by 50% within 60 days
  - Full team adoption (>80% weekly active) by Day 45
  - SSO integration live by end of Q2

  30/60/90 DAY MILESTONES
  Day 7:   Account provisioned, 5 pilot users active
  Day 14:  First check-in, initial feedback collected
  Day 30:  Full team onboarded, baseline metrics captured
  Day 45:  80% adoption target, first ROI measurement
  Day 60:  Review cycle time measured against baseline
  Day 90:  Full health check, QBR prep begins

  STAKEHOLDER ENGAGEMENT PLAN
  Sarah Chen (VP Eng):    Monthly check-in, QBR attendee
  Marcus Webb (Dir):      Bi-weekly sync, primary contact
  Priya Sharma (Staff):   Weekly during onboarding, then as-needed
  David Liu (CTO):        QBR only — keep informed via email
```

[VO] "Structured agenda. Success criteria pulled from what was actually discussed during the sale — not generic 'time to value' goals. Thirty-sixty-ninety milestones. And a stakeholder engagement plan that matches the right cadence to the right person. The CTO who barely showed up during the sales cycle? QBR only. Don't over-engage people who don't want to be over-engaged."

---

### WALKTHROUGH — STEP 3: ONBOARDING PROGRESS (2:40 - 3:15)

[SCREEN] Types: `/cs:onboard-customer meridian`

[VO] "Two weeks in. Let's check onboarding progress."

[SCREEN] Onboarding tracker:

```
ONBOARDING PROGRESS — Meridian Technologies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Day 14 of 90

  MILESTONES
  [x] Day 7:   Account provisioned                 COMPLETE
  [x] Day 7:   5 pilot users active                COMPLETE (8 active)
  [x] Day 14:  First check-in                      TODAY
  [ ] Day 30:  Full team onboarded                  ON TRACK
  [ ] Day 45:  80% adoption                         ON TRACK
  [ ] Day 60:  Review cycle measurement             UPCOMING
  [ ] Day 90:  Full health check                    UPCOMING

  ADOPTION METRICS
  Active users:        8 / 34 licensed (23.5%)
  Features activated:  3 / 7 core features
  Avg daily usage:     12 minutes per user
  Support tickets:     1 (resolved — SSO config question)

  TIME TO VALUE
  First value event:   Day 3 (first AI review completed)
  Target:              50% review time reduction by Day 60
  Current:             Too early to measure (need Day 30 baseline)
```

[VO] "Eight users active against a target of five. Ahead of schedule. Three of seven core features activated — so there's room to drive deeper adoption. One support ticket, already resolved. The time-to-value tracker shows they hit their first value event on day three. These are the metrics that predict whether this account will renew twelve months from now."

---

### WALKTHROUGH — STEP 4: HEALTH CHECK (3:15 - 3:55)

[SCREEN] Types: `/cs:health meridian`

[VO] "Day thirty. First real health check."

[SCREEN] Health score dashboard:

```
HEALTH CHECK — Meridian Technologies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  OVERALL HEALTH: 82/100 — HEALTHY

  DIMENSION SCORES
  1. Product adoption      78/100   [========  ]
     23 of 34 users active. 5 of 7 features used.

  2. Engagement            85/100   [========= ]
     Check-ins on schedule. Marcus responds same-day.

  3. Support               90/100   [========= ]
     2 tickets total. Avg resolution: 4 hours.

  4. Outcomes              75/100   [======== ]
     PR review time down 31% (target: 50% by Day 60).

  5. Relationship          80/100   [========  ]
     Champion strong. Exec sponsor not yet engaged.

  RISKS IDENTIFIED
  - 11 users haven't logged in since Day 5
  - SSO integration not started (promised for Q2)
  - CTO has not been briefed since kickoff

  RECOMMENDED ACTIONS
  1. Run re-engagement for 11 inactive users
  2. Confirm SSO timeline with engineering team
  3. Send CTO a 1-paragraph progress email
```

[VO] "Five dimensions. Product adoption, engagement, support, outcomes, relationship. Eighty-two out of a hundred. Healthy, but with risks. Eleven users dropped off. SSO hasn't started. CTO hasn't been touched. The system doesn't just score — it tells you exactly what to do about each risk."

---

### WALKTHROUGH — STEP 5: QUARTERLY CHECK-IN (3:55 - 4:25)

[SCREEN] Types: `/cs:check-in meridian`

[VO] "Quarterly check-in prep."

[SCREEN] Auto-generated check-in:

```
CHECK-IN PREP — Meridian Technologies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ATTENDEE: Marcus Webb (Director of Platform)
  LAST CHECK-IN: 6 weeks ago

  AUTO-GENERATED AGENDA
  1. Adoption update — 28/34 users active (82%)
  2. Outcomes review — PR time reduced 47% (target: 50%)
  3. Open items: SSO integration status
  4. Upcoming: QBR scheduling, renewal timeline
  5. Feedback collection

  TALKING POINTS
  - Adoption nearly at target. Ask about the 6 inactive users.
  - Outcomes close to goal. Position Day 60 measurement as proof point.
  - SSO is 2 weeks behind the Q2 commitment. Flag proactively.

  RECENT SUPPORT ACTIVITY
  - 4 tickets in last 30 days (all resolved, avg 3.2 hours)
  - 1 feature request: bulk review assignments
  - No escalations
```

[VO] "The agenda writes itself. Usage data, outcomes progress, open items, talking points — all pulled from the system. That SSO flag? It's two weeks behind. The system surfaced that automatically so you don't walk into a check-in blind while the customer is quietly frustrated."

---

### WALKTHROUGH — STEP 6: AT-RISK DETECTION (4:25 - 5:15)

[SCREEN] Time jump. Text overlay: "6 MONTHS LATER"

[SCREEN] Types: `/cs:at-risk`

[VO] "Six months later. Something changed."

[SCREEN] At-risk alert:

```
AT-RISK ACCOUNTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  MERIDIAN TECHNOLOGIES — RISK SCORE: 62/100 (was 82)
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  RISK SIGNALS DETECTED
  [!] Usage declined 34% month-over-month
  [!] Marcus Webb (champion) missed last 2 check-ins
  [!] Support ticket volume spiked: 8 tickets in 2 weeks
  [!] NPS response: 6 (was 8 at Day 90)
  [!] SSO integration still not delivered (Q2 promise broken)

  RISK TIMELINE
  Month 4:   Usage stable, health 80
  Month 5:   Marcus canceled check-in, usage dipped 12%
  Month 6:   Support spike, NPS dropped, usage down 34%

  CHURN PROBABILITY: MODERATE-HIGH

  RECOMMENDED SAVE PLAY
  >> Run /cs:save meridian to activate intervention
```

[VO] "The health score dropped twenty points. Usage down thirty-four percent. The champion — Marcus — missed two check-ins. Support tickets spiked. NPS dropped. And the SSO integration we promised in Q2? Still not delivered. Each of these alone might be noise. Together, they're a pattern. The system flagged it before anyone on the team noticed."

---

### WALKTHROUGH — STEP 7: SAVE PLAY (5:15 - 5:55)

[SCREEN] Types: `/cs:save meridian`

[VO] "Time to intervene."

[SCREEN] Save play activates:

```
SAVE PLAY — Meridian Technologies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  PLAYBOOK SELECTED: Champion Re-engagement + Promise Recovery

  STEP-BY-STEP INTERVENTION
  1. [TODAY]     Direct message to Marcus — personal, not templated.
                 Acknowledge the missed check-ins without pressure.
                 Ask: "What's changed on your side?"

  2. [DAY 2]     Internal escalation — SSO promise breach.
                 Loop in engineering lead. Get realistic timeline.

  3. [DAY 3]     Exec sponsor touch — brief email to David Liu (CTO).
                 1-paragraph update. No alarm. Position as proactive.

  4. [DAY 5]     Support deep-dive — analyze the 8 recent tickets.
                 Pattern: are they bugs, UX confusion, or missing features?

  5. [DAY 7]     Recovery check-in with Marcus. Bring SSO timeline.
                 Bring support analysis. Bring a win (usage data from
                 their top 5 power users).

  6. [DAY 14]    Health re-assessment. Re-score all 5 dimensions.

  HARD GATE: Steps involving customer-facing communication
  require human approval before sending.
```

[VO] "A structured playbook. Not a generic 'reach out to the customer.' Specific steps, specific timing, specific messaging guidance. And notice — the hard gate. Any customer-facing communication in a save play requires human approval. You don't automate a rescue. You guide it."

---

### WALKTHROUGH — STEP 8: QBR AND RENEWAL (5:55 - 7:00)

[SCREEN] Time jump. Text overlay: "MONTH 10"

[SCREEN] Types: `/cs:qbr meridian`

[VO] "The save play worked. Marcus re-engaged. SSO shipped. Health is back to seventy-eight. Time for the QBR."

[SCREEN] QBR output:

```
QBR PREP — Meridian Technologies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  DECK OUTLINE
  1. Executive Summary
  2. Adoption & Usage Trends (12-month view)
  3. Outcomes vs. Success Criteria
  4. Support & Satisfaction
  5. Roadmap Alignment
  6. Renewal Discussion

  KEY METRICS
  - Active users: 31/34 (91% adoption)
  - PR review time: reduced 58% (target was 50%) — EXCEEDED
  - Support satisfaction: 94%
  - NPS: 8 (recovered from 6)

  ROI CALCULATION
  - Engineering hours saved: ~340 hours/quarter
  - At average fully-loaded cost ($85/hr): $28,900/quarter saved
  - Annual value: $115,600 vs. $84,000 contract = 1.38x ROI

  HARD GATE: Customer-facing QBR materials require
  human review before delivery.
```

[VO] "ROI calculated automatically. They're paying eighty-four thousand dollars and getting a hundred and fifteen thousand in engineering time savings. That's a one-point-three-eight x return. That number closes renewals. And again — hard gate on anything customer-facing."

[CUT TO]

[SCREEN] Types: `/cs:renewal meridian`

```
RENEWAL PREP — Meridian Technologies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  CONTRACT
  Current:           $84,000 ARR, 12-month annual
  Renewal date:      2027-03-08 (86 days away)

  RISK ASSESSMENT
  Churn risk:        LOW (health score: 78, trending up)
  Competitive risk:  LOW (no signals detected)
  Champion risk:     MEDIUM (Marcus promoted — new contact TBD)

  PRICING REVIEW
  Current:           $84,000
  Usage-based fair:  $96,000 (31 seats at scale pricing)
  Recommended:       $90,000 (7% uplift, justified by ROI)

  EXPANSION OPPORTUNITY
  - 2 additional teams expressed interest (from Marcus)
  - Potential: 50 additional seats = $140,000 total ARR

  HARD GATE: Contract changes and pricing proposals
  require human approval.
```

[VO] "Renewal prep. Risk assessment — low churn risk, but Marcus got promoted. We need to map the new champion. Pricing recommendation with justification — not a random uplift, a data-backed number tied to their ROI. And an expansion signal — two more teams want in. That's how an eighty-four-thousand-dollar account becomes a hundred-and-forty-thousand-dollar account."

---

### RESULTS RECAP (7:00 - 7:30)

[SCREEN] Timeline view showing the full lifecycle:

```
MERIDIAN TECHNOLOGIES — 12-MONTH LIFECYCLE

  Day 0     Deal closed, handoff received
  Day 1     Kickoff planned
  Day 14    First check-in — on track
  Day 30    Health check — 82/100
  Day 90    QBR prep, NPS collected
  Month 6   At-risk detected — save play activated
  Month 7   Recovered — health 78
  Month 10  QBR delivered, renewal prep started
  Month 12  Renewal + expansion: $84K → $140K ARR
```

[VO] "From handoff to renewal. Twelve months. Every touchpoint tracked. Every risk caught early. Every customer-facing action gated by a human. The at-risk moment at month six? Most companies wouldn't have caught that until the renewal conversation, when it's too late. CS:OS caught it at the first signal and gave the team a playbook to fix it."

---

### CTA (7:30 - 7:45)

[SCREEN] Terminal:

```
CS:OS — open source
github.com/shyftai

Win them. Keep them. Grow them.
```

[TEXT OVERLAY] "Subscribe. Next: How I run my entire startup from Claude Code."

[VO] "CS:OS is free. Open source. Link in the description. Subscribe — the next video is the big one. I'm showing how I run my entire company from one terminal using FOUNDER:OS. Seven frameworks. One cockpit. See you there."

---
---

## Script 3: "How I Run My Entire Startup From Claude Code"

**Total runtime:** ~9 minutes
**OS:** FOUNDER:OS (touching all 7 frameworks)

---

### TITLE CARD (0:00 - 0:05)

[SCREEN] Black background. Text fades in, gold/amber color:

```
HOW I RUN MY ENTIRE STARTUP
FROM CLAUDE CODE

FOUNDER:OS by Shyft AI
```

---

### HOOK (0:05 - 0:35)

[SCREEN] Quick montage — tabs cycling: Notion, Linear, Asana, Google Sheets, Salesforce, QuickBooks, Greenhouse, Mailchimp, Slack, Intercom. Speed increases until it's a blur.

[VO] "I counted my tools last year. Fourteen. Fourteen different apps to run a twelve-person startup. I had a dashboard for my dashboards. I spent more time context-switching between tools than actually making decisions. So I burned it all down."

[SCREEN] All tabs close. Single terminal window fills the screen. Cursor blinks.

[VO] "And built this."

---

### CONTEXT (0:35 - 1:05)

[SCREEN] Terminal. About to boot.

[VO] "This is FOUNDER:OS. It's the cockpit layer that sits on top of seven domain-specific operating systems — GTM, Customer Success, Finance, HR, Content, Investor Relations, and Community. Each one is its own open-source repo. FOUNDER:OS reads from all of them. One terminal. One view. Every decision I need to make, every metric I need to see, every task I need to delegate — all from here."

[TEXT OVERLAY] Bottom-left: "FOUNDER:OS v1.0.0 — open source — github.com/shyftai"

[VO] "Let me show you what a morning looks like."

---

### WALKTHROUGH — STEP 1: MORNING COCKPIT (1:05 - 3:00)

[SCREEN] Types: `/founder:today`

[VO] "Every morning starts with one command."

[SCREEN] FOUNDER:OS boot banner — gold ASCII art, the full block letters. System status panel:

```
FOUNDER:OS v1.0.0                                        by Shyft AI
See everything. Decide fast. Move forward.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Connected OS frameworks:
  [x] GTM:OS        [x] CONTENT:OS     [x] FINANCE:OS
  [x] HR:OS         [x] INVESTOR:OS    [x] COMMUNITY:OS
  [x] CS:OS

  7 frameworks connected · 4 MCP servers · 12 API keys
```

[VO] "Seven frameworks connected. Green across the board. Now watch what happens."

[SCREEN] Morning cockpit renders:

```
TODAY — Tuesday, March 10, 2026
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CASH & RUNWAY (from FINANCE:OS)
  Bank balance:      $2.1M
  Monthly burn:      $187K
  Runway:            11.2 months
  Next payroll:      March 15 — $94K

PIPELINE (from GTM:OS)
  Active deals:      31  |  Value: $624K  |  Weighted: $248K
  Closing this week: 4   |  Total: $89K
  Meetings today:    2   |  Demo at 10:00, Discovery at 14:30

CUSTOMERS (from CS:OS)
  Active accounts:   47
  NRR (trailing):    112%
  At-risk:           2 accounts ($54K ARR)
  Renewals this month: 3

TEAM (from HR:OS)
  Headcount:         12
  Open roles:        2 (Senior Backend, SDR)
  Interviews today:  1 (Senior Backend — final round, 16:00)

FUNDRAISE (from INVESTOR:OS)
  Status:            Series A — active
  Pipeline:          14 firms contacted, 6 meetings done, 3 interested
  Next meeting:      Sequoia — Thursday 11:00

CONTENT (from CONTENT:OS)
  Publishing today:  1 blog post (scheduled 10:00)
  Newsletter:        Thursday (draft ready, needs review)
  Social queue:      3 posts scheduled this week

COMMUNITY (from COMMUNITY:OS)
  Active members:    2,340
  Engagement (7d):   18.4% (up from 15.2%)
  Open threads:      12 (3 need founder response)
```

[VO] "One screen. Everything. Cash position and runway from Finance OS. I've got eleven months — not urgent, but I'm watching it. Pipeline from GTM OS — four deals closing this week, two meetings today. Customer health from CS OS — two at-risk accounts, gotta keep an eye on those. HR says I have a final-round interview at four. Investor OS — Sequoia on Thursday. Content OS — blog post goes live at ten. Community — three threads need my personal response."

[SCREEN] OKR progress section appears:

```
Q1 OKRs
  1. Hit $1.2M ARR          [================    ] 78%  ($936K)
  2. Ship V2 platform       [==============      ] 70%  (7/10 features)
  3. Close Series A         [=========           ] 45%  (3 interested / need term sheet)
```

[VO] "OKRs. Not in a slide I update once a quarter. Live. Seventy-eight percent to ARR target. Platform at seventy percent. Series A at forty-five — need to close that gap."

[SCREEN] Priorities and alerts:

```
TODAY'S PRIORITIES
  1. [CRITICAL] Prep for Sequoia meeting Thursday
  2. [HIGH]     Review at-risk accounts with CS
  3. [HIGH]     Final round interview — Senior Backend
  4. [MEDIUM]   Review newsletter draft
  5. [LOW]      Respond to 3 community threads

CRITICAL ALERTS
  [!] Runway below 12 months — fundraise timeline matters
  [!] 2 at-risk CS accounts worth $54K ARR combined
```

[VO] "Priorities ranked. Alerts surfaced. I haven't opened a browser. I haven't checked Slack. I know exactly what matters today in thirty seconds."

---

### WALKTHROUGH — STEP 2: MAKE A DECISION (3:00 - 4:00)

[SCREEN] Types: `/founder:decide`

[VO] "Let's say I need to make a call. The two at-risk accounts — do I personally intervene, or let the CS process handle it?"

[SCREEN] Decision framework activates:

```
DECISION FRAMEWORK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  What's the decision?
  > Should I personally intervene on the 2 at-risk accounts
    or let the CS:OS save plays run?

  TYPE CLASSIFICATION
  Type 2 — Reversible decision.
  Apply the 70% rule: decide with 70% of the information.

  CONTEXT
  - Meridian ($34K ARR): Champion promoted, usage dipping.
    CS:OS save play activated 5 days ago. Early signals positive.
  - Bolt Labs ($20K ARR): Support spike, no champion identified.
    CS:OS save play activated 2 days ago. No response yet.

  ANALYSIS
  Meridian: Save play is working. Founder intervention now
  could undermine CS team's authority. RECOMMENDATION: Monitor.

  Bolt Labs: No champion = structural risk. CS team may not
  have the relationship depth. RECOMMENDATION: Founder steps in.

  PRE-MORTEM
  If I intervene on both: CS team feels micromanaged, I lose
  3 hours this week before the Sequoia meeting.
  If I skip both: Bolt Labs churns silently.

  DECISION
  >> Intervene on Bolt Labs only. Delegate Meridian to CS.
  >> Route: /founder:delegate to CS:OS for Meridian monitoring
```

[VO] "The decision framework kicks in. First — is this a Type 1 or Type 2 decision? Type 2. Reversible. So I use the seventy-percent rule — don't overthink it. The system pulls context on both accounts. Meridian's save play is already working. Bolt Labs has no champion — that's a structural problem the CS team can't solve alone. Pre-mortem: if I jump into both, I lose three hours before my most important investor meeting. Decision: intervene on Bolt only. Delegate Meridian monitoring back to CS. Structured. Fast. Defensible."

---

### WALKTHROUGH — STEP 3: DELEGATE (4:00 - 4:50)

[SCREEN] Types: `/founder:delegate`

[VO] "Now I route the work."

[SCREEN] Delegation interface:

```
DELEGATE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  What's the task?
  > Draft and send a new outbound campaign targeting DevOps
    leads at enterprise companies. Q1 push.

  ROUTING ANALYSIS
  This is a GTM execution task.
  Route to: GTM:OS
  Workspace: enterprise-q1

  DELEGATION BRIEF
  Task:         New outbound campaign — DevOps enterprise
  Owner:        GTM:OS (auto mode)
  Deadline:     March 14
  Success:      Campaign live, 500 leads loaded, sequence approved
  Context:      Q1 ARR push — need pipeline fast
  Constraints:  Stay within existing ICP. Don't target current customers.

  TRACKED IN: /DELEGATION.md
  STATUS: Delegated — awaiting completion

  >> To execute: open GTM:OS and run /gtm:new-campaign enterprise-q1
```

[VO] "I describe the task in plain language. The system identifies it as a GTM execution task, routes it to GTM:OS, writes a delegation brief with deadline and success criteria, and tracks it. I don't need to open GTM:OS right now. When I do — or when someone on my team does — the brief is waiting."

---

### WALKTHROUGH — STEP 4: QUICK CUT TO GTM:OS (4:50 - 5:20)

[SCREEN] New terminal tab. Types: `/gtm:write enterprise-q1`

[TEXT OVERLAY] "Quick cut: GTM:OS executing the delegated task"

[VO] "Quick cut. Here's what happens on the other side. Someone opens GTM:OS, the delegation brief is loaded, and the campaign builds itself."

[SCREEN] Fast montage — GTM:OS writing a sequence, validation running (5/5 PASS), ship check showing all green. Speed: 2x.

[VO] "Sequence written. Validated. Ship check passed. The delegated task is done. FOUNDER:OS will pick this up in the next /founder:today and show it as completed."

---

### WALKTHROUGH — STEP 5: WEEKLY REVIEW (5:20 - 6:30)

[SCREEN] Back to FOUNDER:OS terminal. Types: `/founder:weekly`

[TEXT OVERLAY] "FRIDAY"

[VO] "Friday. Weekly review. This is the most important thirty minutes of my week."

[SCREEN] Weekly review renders:

```
WEEKLY REVIEW — Week of March 9, 2026
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

WINS
  1. Closed Apex Industries — $42K ARR (GTM:OS)
  2. Sequoia meeting went well — follow-up scheduled (INVESTOR:OS)
  3. Senior Backend engineer accepted offer (HR:OS)
  4. Blog post hit 12K views, 340 signups (CONTENT:OS)
  5. Meridian save play successful — health back to 78 (CS:OS)

MISSES
  1. Bolt Labs churned — $20K ARR lost (CS:OS)
  2. Newsletter delayed to next week (CONTENT:OS)
  3. Community AMA postponed — scheduling conflict (COMMUNITY:OS)

METRICS MOVEMENT
  ARR:             $936K → $958K (+$42K won, -$20K churned)
  Pipeline:        $624K → $587K (closed $42K, added $5K)
  Runway:          11.2 → 11.0 months
  NRR:             112% → 109%
  Headcount:       12 → 13 (backend eng starts Monday)

OKR UPDATES
  1. $1.2M ARR     78% → 80%  [on track]
  2. V2 Platform   70% → 75%  [on track]
  3. Series A      45% → 55%  [needs acceleration]

DELEGATION STATUS
  [x] GTM campaign (enterprise-q1) — COMPLETE, live
  [x] CS save play (Meridian) — COMPLETE, recovered
  [-] CS save play (Bolt Labs) — FAILED, churned
  [ ] Content newsletter — DELAYED

BLOCKERS
  - Series A needs 2 more partner meetings to reach term sheet
  - Pipeline replenishment needed — $37K net negative this week

NEXT WEEK PRIORITIES
  1. [CRITICAL] Schedule 2 more VC partner meetings
  2. [HIGH]     Launch enterprise outbound campaign (delegated, done)
  3. [HIGH]     Backfill pipeline — run new GTM campaign
  4. [MEDIUM]   Onboard new backend engineer
  5. [MEDIUM]   Ship newsletter
```

[VO] "Everything that happened this week. Across every function. Wins — closed a deal, Sequoia went well, hired someone, content performed, saved an account. Misses — lost Bolt Labs, newsletter slipped, AMA got postponed. Metrics moved. ARR up net twenty-two K. NRR dipped because of the churn. Runway ticked down. OKR progress updated automatically."

[VO] "And look at the delegation tracker. Campaign — complete. Meridian save play — complete. Bolt Labs — failed. Newsletter — delayed. I can see what got done and what didn't without chasing anyone."

[VO] "Blockers and priorities for next week write themselves based on what happened this week. Series A needs acceleration. Pipeline needs replenishment. New hire starts Monday."

---

### WALKTHROUGH — STEP 6: METRICS DASHBOARD (6:30 - 7:15)

[SCREEN] Types: `/founder:metrics`

[VO] "One more. The metrics dashboard."

[SCREEN] Dashboard renders:

```
FOUNDER METRICS DASHBOARD
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

NORTH STAR
  ARR: $958K       Target: $1.2M by March 31
  Gap: $242K       Needed: $242K in 21 days
  Trend: +$22K/week avg (need $80K/week to hit target)

DEPARTMENTAL KPIs
  ┌─────────────────────────────────────────────────────┐
  │ GTM:OS                                              │
  │   Pipeline value:     $587K                         │
  │   Win rate:           28% (trailing 90d)            │
  │   Meetings booked:    14 this month                 │
  │   Response rate:      4.2% (above 3% benchmark)    │
  │                                                     │
  │ CS:OS                                               │
  │   NRR:                109%                          │
  │   Gross retention:    94%                           │
  │   Active accounts:    46 (was 47)                   │
  │   CSAT:               4.3/5                         │
  │                                                     │
  │ FINANCE:OS                                          │
  │   Burn:               $187K/month                   │
  │   Runway:             11.0 months                   │
  │   Revenue growth:     +18% QoQ                      │
  │   Gross margin:       82%                           │
  │                                                     │
  │ HR:OS                                               │
  │   Headcount:          13                            │
  │   Open roles:         1 (SDR)                       │
  │   Time to hire:       34 days avg                   │
  │   Retention:          100% (trailing 12m)           │
  │                                                     │
  │ CONTENT:OS                                          │
  │   Monthly views:      48K (up 22%)                  │
  │   Email subscribers:  3,240                         │
  │   Conversion rate:    2.8%                          │
  │                                                     │
  │ INVESTOR:OS                                         │
  │   Firms contacted:    14                            │
  │   Active conversations: 3                           │
  │   Next milestone:     Term sheet                    │
  │                                                     │
  │ COMMUNITY:OS                                        │
  │   Members:            2,340                         │
  │   Weekly engagement:  18.4%                         │
  │   NPS:                62                            │
  └─────────────────────────────────────────────────────┘

TRENDS (8-week)
  ARR:       $870K → $958K        ▲ +10.1%
  Pipeline:  $510K → $587K        ▲ +15.1%
  Burn:      $178K → $187K        ▲ +5.1% (watch)
  NRR:       115%  → 109%         ▼ -5.2% (watch)
  Runway:    12.8  → 11.0 months  ▼ (expected, pre-fundraise)
```

[VO] "North star metric — ARR. Nine-fifty-eight K against a one-point-two M target. The math says I need eighty K a week to hit it. That's aggressive. The system flags it, I decide whether to revise the target or push harder. Every department, one view. GTM win rate, CS retention, finance burn, HR headcount, content growth, fundraise status, community engagement. Eight-week trends at the bottom. Burn is ticking up — flagged. NRR dipped — flagged. Runway declining is expected because we're pre-fundraise."

---

### WALKTHROUGH — STEP 7: THE ONE-TERMINAL PHILOSOPHY (7:15 - 7:55)

[SCREEN] Terminal. User scrolls through the workspace file tree:

```
/c/Antigravity/
  FOUNDEROS/         ← cockpit (you are here)
  GTMOS/             ← go-to-market
  CSOS/              ← customer success
  FINANCEOS/         ← finance
  HROS/              ← hiring & team
  INVESTOROS/        ← fundraising
  CONTENTOS/         ← content
  COMMUNITYOS/       ← community
```

[VO] "This is my entire company. Eight repos. All markdown. All version-controlled. All readable by Claude Code. No vendor lock-in. No $200-per-seat SaaS bill. No integration hell where Salesforce talks to Slack talks to HubSpot talks to a Zap that breaks every Tuesday."

[SCREEN] Terminal. Clean. Cursor blinking.

[VO] "I open one terminal. I type one command. And I see everything I need to see to run my company. The decisions happen faster because the context is already there. The delegation works because the receiving system already has the brief. The reviews write themselves because the data is structured."

[TEXT OVERLAY] "One terminal. Seven frameworks. Zero context-switching."

[VO] "That's the philosophy. Not 'AI will replace your team.' Your team still does the work. This just makes sure the right work gets done, nothing falls through the cracks, and the founder isn't spending half their day assembling information from six different tools just to figure out what to focus on."

---

### RESULTS RECAP (7:55 - 8:25)

[SCREEN] Summary card:

```
WHAT WE JUST DID

  /founder:today     — Full company status in 30 seconds
  /founder:decide    — Structured decision with framework
  /founder:delegate  — Route work to the right OS
  /founder:weekly    — Complete weekly review, auto-generated
  /founder:metrics   — Cross-functional dashboard

  7 OS frameworks. 1 cockpit. 0 browser tabs.

  Open source. Free. Runs in Claude Code.
```

[VO] "Five commands. Morning cockpit, a decision, a delegation, a weekly review, and a metrics dashboard. That covers about eighty percent of what I do as a founder in any given week. And it all ran from one terminal in nine minutes."

---

### CTA (8:25 - 8:45)

[SCREEN] Terminal. Final text:

```
FOUNDER:OS — open source
github.com/shyftai

Antigravity OS Ecosystem:
  GTM:OS · CS:OS · FINANCE:OS · HR:OS
  INVESTOR:OS · CONTENT:OS · COMMUNITY:OS

See everything. Decide fast. Move forward.
```

[TEXT OVERLAY] "Subscribe for weekly deep dives into each OS."

[VO] "Everything you just saw is free and open source. Links in the description. Clone FOUNDER:OS, connect it to whichever domain OS you need, and run /founder:today. If this is the first video you're seeing, go back and watch the GTM:OS and CS:OS walkthroughs. They show the domain-level workflows in detail. Subscribe — I'm dropping a new deep dive every week. See you in the next one."

---
---

## Production Notes

### Recording Tips

- **Screen resolution:** Record at 1920x1080 or 2560x1440. Terminal should fill 80-90% of the screen. Dark terminal theme (Dracula, One Dark, or native dark).
- **Font size:** 16-18px minimum in terminal. Viewers watch on mobile — small text kills engagement.
- **Typing speed:** Type at a natural pace. Don't rush the commands. Pause for 1-2 seconds after each command before the output renders. This gives viewers time to read what you typed.
- **Output rendering:** If possible, add a slight delay to output rendering so it scrolls at a readable pace. Instant dumps are hard to follow. Alternatively, use post-production pacing.
- **VO recording:** Record VO separately from screen capture. Quiet room, close mic, conversational tone. Not a podcast voice. Not a tutorial voice. Talk like you're showing a friend.
- **Multiple takes per section:** Record each walkthrough step as a separate take. Easier to edit. Easier to re-record one section without redoing the whole video.

### Editing Guidance

- **Pacing:** Deep dives should breathe. Don't cut every pause. Let the terminal output sit on screen for 2-3 seconds before moving to the next VO line.
- **Zoom and highlight:** When calling attention to a specific line (like the hard gate, a health score, or a risk signal), zoom in 120-140% on that section. Add a subtle highlight box or underline.
- **Transitions between steps:** Simple crossfade or hard cut. No fancy transitions. This is a developer/founder tool — keep the editing minimal and clean.
- **Time jumps:** For Script 2 (CS:OS) and Script 3 (FOUNDER:OS), use text overlays like "6 MONTHS LATER" or "FRIDAY" to indicate time skips. Brief fade-to-black works.
- **Background music:** Very light, lo-fi or ambient. Low volume. Drop it entirely during complex output sections. Music should be felt, not heard.
- **Lower thirds:** Use consistent lower-third overlay for OS name, version, and github link. Appears at the start of each walkthrough, disappears after 10 seconds.

### Thumbnail Suggestions

**Script 1 (GTM:OS):**
- Terminal screenshot showing the `/gtm:ship` hard gate with "APPROVED"
- Text overlay: "10-Minute Outbound Campaign"
- Color accent: Orange (GTM:OS brand color)

**Script 2 (CS:OS):**
- Terminal screenshot showing the at-risk alert with health score dropping
- Text overlay: "Handoff to Renewal"
- Color accent: Blue (CS:OS brand color)

**Script 3 (FOUNDER:OS):**
- Terminal screenshot showing the full `/founder:today` cockpit with all 7 frameworks
- Text overlay: "One Terminal. Entire Startup."
- Color accent: Gold (FOUNDER:OS brand color)

**General thumbnail rules:**
- Face in thumbnail (founder) increases CTR 30-40%
- High contrast text — white or yellow on dark background
- No more than 5-6 words on the thumbnail
- Terminal screenshots should be cropped to the most impactful 3-4 lines, not the full output
