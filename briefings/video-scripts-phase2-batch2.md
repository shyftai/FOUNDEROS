# Video Scripts — Phase 2, Batch 2

> Antigravity OS ecosystem by Shyft AI
> Format: Deep-dive screen recordings, founder-narrated, 5-10 minutes each
> Platform: YouTube (landscape 1920x1080)
> Style: Founder showing their actual setup in Claude Code. Real, unpolished, passionate.

---

## Script 4: "The AI Content Engine: Strategy to Publish"

**Total runtime:** ~7 minutes

---

### TITLE CARD (0:00 - 0:05)

[SCREEN] Black background. Text fades in:

```
THE AI CONTENT ENGINE
Strategy to Publish in One Terminal

CONTENT:OS by Shyft AI
```

[TEXT OVERLAY] Small Shyft AI logo, bottom right.

---

### HOOK (0:05 - 0:30)

[SCREEN] LinkedIn feed scrolling. Ghost profiles — founders with one post from 6 months ago. Then a "content calendar" Google Sheet with most cells empty. Red overdue tags everywhere.

[VO] "Every founder I talk to says the same thing. 'I know I should be posting. I have ideas. I just don't have time.' And I get it. Because content isn't one thing — it's twelve. You need a strategy. You need pillars. You need to write the thing. Then you need to chop it up for LinkedIn, for Twitter, for your newsletter. And then you need to do it again next week. And the week after. Most people give up after post three. I did. Until I built this."

[TEXT OVERLAY] "Most founders quit content after 3 posts."

---

### CONTEXT (0:30 - 1:00)

[SCREEN] Terminal open. Clean. VS Code sidebar showing the CONTENT:OS repo structure — `.claude/commands/content/` folder with all the command files visible.

[VO] "This is CONTENT:OS. It's one of eight operating systems in the Antigravity ecosystem. It runs entirely in Claude Code — no app, no login, no monthly fee. What I'm going to show you is the full workflow. From setting up a brand new content workspace to having a month of content planned, written, repurposed, and measured. End to end. In one terminal session. Let's go."

[TEXT OVERLAY] "Full workflow: onboard > strategy > calendar > write > repurpose > analytics"

---

### WALKTHROUGH (1:00 - 6:30)

#### Step 1: Onboard (1:00 - 2:10)

[SCREEN] Terminal. User types: `/content:onboard synthwave`

[VO] "First, I set up a workspace. I'm going to use a fake company called Synthwave — they make developer tools for API monitoring."

[SCREEN] CONTENT:OS boot banner appears — the ASCII art, version number, "Research it. Write it. Publish it. Measure it. by Shyft AI".

[VO] "The boot sequence loads. This is the CONTENT:OS banner — every OS in the ecosystem has its own."

[SCREEN] Role selection appears:

```
  What's your role?

  >> Content Creator / Writer
  >> Content Strategist
  >> Social Media Manager
  >> SEO Specialist
  >> Head of Content
  >> Agency
```

User selects "Head of Content".

[VO] "It asks my role first. This changes the depth of the setup. A content creator gets a lighter onboard focused on writing and briefs. A head of content gets the full depth — strategy, calendar, measurement, team features."

[SCREEN] Collaboration mode: selects "Solo". Execution mode: selects "Interactive".

[SCREEN] Brand setup begins. Prompts appear one at a time:
- "Company name?" — types "Synthwave"
- "What do you do?" — types "API monitoring for developer teams"
- "Target audience?" — types "Engineering leads and DevOps teams at Series A-C startups"

[VO] "Brand basics. Who you are, what you do, who you serve. Simple questions, but CONTENT:OS stores these as structured data, not just notes. Every piece of content it writes later will reference these."

[SCREEN] Content pillars definition:

```
  CONTENT PILLARS

  1. API Reliability      — monitoring best practices, uptime
  2. Developer Experience  — DX improvements, tooling
  3. Engineering Culture   — team scaling, incident response
  4. Product Updates       — releases, case studies
```

[VO] "Content pillars. These are the four lanes everything falls into. No more random one-off posts. Every piece of content maps to a pillar."

[SCREEN] Tone of voice setup:

```
  TONE OF VOICE

  Voice:     Technical but accessible
  Persona:   Senior engineer who's seen things
  Style:     Direct. No corporate fluff. Code examples welcome.
  Avoid:     Buzzwords, "leverage", "synergy", "game-changing"
  Platforms:  Blog, LinkedIn, Twitter/X, YouTube
```

[VO] "Tone of voice. This is the DNA of your brand's writing. And here's what matters — this isn't a one-time exercise that lives in a Google Doc nobody reads. Every single piece of content CONTENT:OS writes gets checked against these rules. Automatically."

[SCREEN] Workspace confirmation:

```
  Workspace created: /workspaces/synthwave/

  Files generated:
    BRAND.md        — company identity
    AUDIENCE.md     — target segments
    PILLARS.md      — content pillars
    TOV.md          — tone of voice
    CHANNELS.md     — platform config
    CALENDAR.md     — empty, ready to fill
    PERFORMANCE.md  — metrics baseline
```

[VO] "Workspace created. All structured. All connected. Now let's fill it."

---

#### Step 2: Strategy (2:10 - 3:00)

[SCREEN] User types: `/content:brief synthwave "API monitoring for startups" --channel blog`

[VO] "Now I create a content brief. I give it a topic and a channel."

[SCREEN] Brief generation begins. The system loads BRAND.md, AUDIENCE.md, PILLARS.md, TOV.md — each file name flashes as it loads.

[VO] "Watch what happens. It loads every context file we just created. Brand. Audience. Pillars. Tone of voice. All of it informs the brief."

[SCREEN] Brief renders:

```
  CONTENT BRIEF

  Title:      "Why Your API Monitoring Is Lying to You"
  Pillar:     API Reliability (#1)
  Channel:    Blog (long-form)
  Audience:   Engineering leads at Series A-C
  Goal:       Thought leadership — position Synthwave
  Keywords:   api monitoring, uptime monitoring, API observability
  Outline:
    1. The false confidence of green dashboards
    2. 3 metrics that actually matter
    3. Real examples of silent failures
    4. What good monitoring looks like
  CTA:        Try Synthwave's free tier
  Word count: 1200-1500
```

[VO] "A full brief. Title. Pillar mapping. Target audience. Keyword clusters. Structured outline. CTA. Word count target. This isn't a vague idea — it's a spec."

---

#### Step 3: Calendar (3:00 - 3:40)

[SCREEN] User types: `/content:calendar synthwave --view month`

[VO] "Let's see the calendar."

[SCREEN] Calendar renders — a month grid view:

```
  ┌─ CONTENT CALENDAR ─── MARCH 2026 ──────────────┐
  │                                                   │
  │  MON    TUE    WED    THU    FRI    SAT   SUN    │
  │  ┌──────┬──────┬──────┬──────┬──────┬─────┬────┐ │
  │  │      │      │ LI   │      │ Blog │     │    │ │
  │  │      │      │ post │      │ #1   │     │    │ │
  │  ├──────┼──────┼──────┼──────┼──────┼─────┼────┤ │
  │  │ TW   │      │ LI   │      │ NL   │     │    │ │
  │  │ thrd │      │ post │      │ send │     │    │ │
  │  ├──────┼──────┼──────┼──────┼──────┼─────┼────┤ │
  │  │      │      │ LI   │ YT   │ Blog │     │    │ │
  │  │      │      │ post │ scpt │ #2   │     │    │ │
  │  ├──────┼──────┼──────┼──────┼──────┼─────┼────┤ │
  │  │ TW   │      │ LI   │      │ NL   │     │    │ │
  │  │ thrd │      │ post │      │ send │     │    │ │
  │  └──────┴──────┴──────┴──────┴──────┴─────┴────┘ │
  │                                                   │
  │  THIS MONTH: 12 items planned                     │
  │  PIPELINE:   2 briefs ready | 1 draft in progress │
  │  PILLARS:    Reliability (4) · DX (3) · Culture   │
  │              (3) · Product (2)                     │
  │                                                   │
  └───────────────────────────────────────────────────┘
```

[VO] "A month of content. Mapped to channels. Blog posts on Fridays, LinkedIn on Wednesdays, Twitter threads on Mondays, newsletters biweekly. Every piece is connected to a pillar. Balanced distribution. And look at the bottom — pipeline status and pillar coverage. You can see at a glance if you're leaning too hard on one topic."

---

#### Step 4: Write (3:40 - 4:50)

[SCREEN] User types: `/content:write synthwave "api-monitoring-lying" --channel blog`

[VO] "Now we write. I point it at the brief we just created."

[SCREEN] Loading sequence:

```
  << CONTENT:OS // WRITE >>

  Loading context...
    BRAND.md      — loaded
    AUDIENCE.md   — loaded
    TOV.md        — loaded
    PILLARS.md    — loaded
    LEARNINGS.md  — loaded (0 prior posts — first one)
    Brief         — "api-monitoring-lying" loaded
    Channel specs — blog format loaded
```

[VO] "Watch the context loading. It pulls brand, audience, tone of voice, pillars, learnings from past content — we don't have any yet, but as you publish more, it learns what works — and the brief. Everything feeds into the writing."

[SCREEN] Article begins rendering. Title, then paragraph by paragraph. Speed up this section — show the text flowing, not every word.

```
  # Why Your API Monitoring Is Lying to You

  Your dashboard says everything is green. Your uptime page
  shows 99.97%. Your on-call engineer slept through the night.

  And yet — three of your largest customers filed support
  tickets this morning about slow response times that your
  monitoring never caught.

  Here's the uncomfortable truth...
```

[VO] "The article writes. And it's not generic — it sounds like a senior engineer who's been burned by bad monitoring. That's the tone of voice profile doing its job."

[SCREEN] Quality gates run:

```
  QUALITY GATES
    [x] Brief check     — matches outline, word count 1,340
    [x] Brand check     — TOV.md rules applied
    [x] Audience check  — engineering leads, right level
    [x] SEO check       — keyword in H1, meta title, 3 internal links
    [x] Readability     — Grade 8 avg, no jargon overload
    [x] Source check    — 2 claims cited, no fabrication
    [x] Channel check   — blog format, headers, scannable

  >> Approve? (approve / edit / rewrite / reject)
```

[VO] "Quality gates. This is the part I care about most. Seven checks. Does it match the brief? Does it sound like us? Is the SEO right? Are the claims actually cited or did it make something up? Readability score. Channel formatting. All green. Nothing ships without passing these gates."

[SCREEN] User types: `approve`

```
  Content saved: content/approved/api-monitoring-lying.md
  Added to CALENDAR.md: March 13 (Blog)

  >> Tip: /content:repurpose — transform for other channels
```

[VO] "Approved. Saved. Added to the calendar. And it's already suggesting the next move — repurpose it."

---

#### Step 5: Repurpose (4:50 - 5:50)

[SCREEN] User types: `/content:repurpose synthwave api-monitoring-lying --channels linkedin,twitter,youtube`

[VO] "This is where it gets wild. I take that one blog post and turn it into content for three more platforms. One command."

[SCREEN] Loading:

```
  << CONTENT:OS // REPURPOSE >>

  Source: "Why Your API Monitoring Is Lying to You" (blog, 1,340 words)
  Targets: LinkedIn post, Twitter/X thread, YouTube script outline
  Loading channel specs...
```

[SCREEN] Repurposed content appears section by section:

```
  ── ORIGINAL (Blog) ──────────────────────────────────
  "Why Your API Monitoring Is Lying to You"
  1,340 words | Published March 13

  ── LINKEDIN POST ────────────────────────────────────

  Your monitoring dashboard is green.
  Your customers are filing tickets.

  Something doesn't add up.

  I spent 6 years trusting uptime dashboards that were
  measuring the wrong things. Here's what I learned:

  1. Uptime != user experience
  2. P50 latency hides P99 disasters
  3. Synthetic checks don't catch real-world edge cases

  The fix isn't more monitoring. It's better questions.

  Full breakdown on our blog (link in comments).

  #APIDevelopment #Monitoring #DevOps

  ── TWITTER/X THREAD ─────────────────────────────────

  1/ Your API monitoring is lying to you.

  Your dashboard says 99.97% uptime. Your customers say
  "it's slow." Both are telling the truth.

  Here's why (thread):

  2/ Most monitoring tools measure availability.
  "Can I reach the endpoint?" Yes/No.

  But availability != performance != user experience.

  3/ P50 latency: 45ms. Looks great.
  P99 latency: 2,400ms. Your top 1% of users are
  waiting 2.4 seconds per call.

  That 1% is often your biggest customers.

  4/ The fix: monitor what your users actually feel.
  - P95/P99 latency, not just P50
  - Error rates by endpoint, not aggregate
  - Time to first byte for real user flows

  5/ We built Synthwave to answer the question dashboards
  don't: "Are my users happy right now?"

  Free tier. No credit card. Link below.

  ── YOUTUBE SCRIPT OUTLINE ───────────────────────────

  Title: "Your API Monitoring Is Lying to You"
  Length: 3-5 min
  Hook: "Every dashboard in this screenshot is green.
         And yet we had 47 support tickets this morning."
  Sections:
    1. The Green Dashboard Problem (1 min)
    2. What Monitoring Actually Misses (1.5 min)
    3. 3 Metrics You Should Track Instead (1.5 min)
    4. Live Demo — Synthwave Dashboard (1 min)
  CTA: Subscribe + free tier link

  ── ────────────────────────────────────────────────────

  >> Approve all / Edit / Select specific
```

[VO] "Look at that. Same core insight — different format for every platform. The LinkedIn post leads with a hook and keeps it scannable. The Twitter thread breaks the argument into numbered tweets. The YouTube outline has a hook, sections, and a CTA. And notice — the LinkedIn post doesn't just have different formatting. It has a different hook. A different angle. Because CONTENT:OS knows that what works on a blog doesn't work on LinkedIn. The channel specs are baked in."

[SCREEN] User types: `approve all`

```
  Saved 3 versions to content/approved/
    linkedin-api-monitoring-lying.md
    twitter-api-monitoring-lying.md
    youtube-api-monitoring-lying.md

  Added to CALENDAR.md:
    March 12 (LinkedIn)
    March 10 (Twitter thread)
    YouTube script — queued for production
```

[VO] "Three pieces of content. All approved. All added to the calendar. One blog post became four pieces of content. Do that every week and you have sixteen posts a month from writing one article."

---

#### Step 6: Analytics (5:50 - 6:30)

[SCREEN] User types: `/content:analytics synthwave --period 30d`

[VO] "Fast forward a month. Let's check how it's all performing."

[SCREEN] Analytics dashboard renders:

```
  ┌─ ANALYTICS ─── Last 30 days ─────────────────────┐
  │                                                    │
  │  OVERVIEW                                         │
  │  Total reach: 14,200 (+82% vs prev period)        │
  │  Total engagement: 847 (+64%)                     │
  │  New subscribers: 112 (+41%)                      │
  │  Content published: 14 pieces                     │
  │                                                    │
  │  BY CHANNEL                                       │
  │  Blog:    2,100 sessions (+120%)                  │
  │    Top: "API Monitoring Is Lying" — 890 sessions  │
  │  LinkedIn: 8,400 impressions (+74%)               │
  │    Top: API monitoring post — 312 engagements     │
  │  Twitter:  3,200 impressions (+45%)               │
  │    Top: Monitoring thread — 67 retweets           │
  │  Newsletter: 489 subscribers, 52% open rate       │
  │                                                    │
  │  BY PILLAR                                        │
  │  API Reliability:    62% of engagement             │
  │  Developer Exp:      24% of engagement             │
  │  Eng Culture:        11% of engagement             │
  │  Product Updates:     3% of engagement             │
  │                                                    │
  │  CONTENT GAP ANALYSIS                             │
  │  - "API Reliability" is your best performer       │
  │    → double down: 2 more posts this pillar        │
  │  - "Product Updates" underperforming              │
  │    → try case study format instead of release     │
  │      notes                                        │
  │  - Missing: no video content published yet        │
  │    → YouTube script is queued — prioritize it     │
  │                                                    │
  │  RECOMMENDATIONS                                  │
  │  1. Write a follow-up to "API Monitoring" (high   │
  │     engagement signal)                            │
  │  2. Shift Product pillar to customer stories      │
  │  3. Publish the YouTube script — video gap        │
  │                                                    │
  └────────────────────────────────────────────────────┘
```

[VO] "Performance dashboard. Reach up eighty-two percent. Engagement up sixty-four percent. And here's what I love — it doesn't just show you numbers. It shows you what to do next. The API reliability pillar is crushing it — write more. Product updates are flat — try case studies instead. No video yet — that YouTube script we generated is sitting in the queue. It closes the loop. Strategy feeds content feeds analytics feeds back into strategy."

---

### RESULTS RECAP (6:30 - 7:00)

[SCREEN] Split screen — left side shows the terminal with all the commands we ran, right side shows a summary:

```
  SESSION RECAP

  1. Workspace created     — brand, audience, pillars, TOV
  2. Brief generated       — structured, keyword-targeted
  3. Calendar planned      — 12 pieces across 4 channels
  4. Blog article written  — 1,340 words, all gates passed
  5. Repurposed to 3 more  — LinkedIn, Twitter, YouTube
  6. Analytics reviewed    — gaps identified, next moves clear

  Total content pieces: 4 from 1 writing session
  Time: ~15 minutes of actual input
```

[VO] "Let me recap what just happened. We went from zero to a fully configured content workspace, a strategic brief, a month-long calendar, a published blog post, three repurposed versions for different platforms, and a performance dashboard with actionable next steps. One terminal. One session. Four pieces of content from writing one article. Most founders know they should post content. Few do it consistently. This system makes it impossible not to be consistent — because the hard part isn't the writing. It's the system. And now the system runs itself."

---

### CTA (7:00 - 7:15)

[SCREEN] Terminal. CONTENT:OS banner visible at top.

```
  github.com/shyftai

  Clone it. Run /content:onboard. Your first post in 10 minutes.
```

[TEXT OVERLAY] "CONTENT:OS — free and open source"

[VO] "CONTENT:OS is free and open source. Clone the repo, run /content:onboard, and have your first piece of content drafted in ten minutes. Subscribe for the next video where I show you how INVESTOR:OS turned my fundraise from chaos into a pipeline. Link in the description."

---

---

## Script 5: "Fundraising With AI: Pipeline to Term Sheet"

**Total runtime:** ~8 minutes

---

### TITLE CARD (0:00 - 0:05)

[SCREEN] Black background. Text fades in:

```
FUNDRAISING WITH AI
Pipeline to Term Sheet

INVESTOR:OS by Shyft AI
```

[TEXT OVERLAY] Small Shyft AI logo, bottom right.

---

### HOOK (0:05 - 0:35)

[SCREEN] A founder's inbox — 47 investor emails in various states. Some replied, some ghosted, some "let's circle back in Q2." A messy Notion board with investor names and question marks. Then a Google Sheet titled "Fundraise Tracker" with columns like "Vibe Check" and "Maybe Interested?"

[VO] "Fundraising is a sales process. But most founders treat it like a creative writing exercise. They blast out a pitch deck to fifty investors with the same generic email. They track follow-ups in a spreadsheet with a column called 'vibes.' They have no idea what their conversion rate is from intro to meeting. They don't know which investors actually match their stage and sector. And then they wonder why the raise is taking eight months instead of four. INVESTOR:OS treats fundraising like what it is — a pipeline. Because that's what it is."

[TEXT OVERLAY] "Fundraising is a pipeline. Treat it like one."

---

### CONTEXT (0:35 - 1:05)

[SCREEN] Terminal. VS Code sidebar showing the INVESTOR:OS repo — `_template/` folder with THESIS.md, PIPELINE.md, INVESTORS.md, DATA-ROOM.md, etc.

[VO] "This is INVESTOR:OS. It's the fundraising operating system in the Antigravity ecosystem. Everything runs in Claude Code. No CRM subscription. No investor management platform. Your fundraise, structured as files you own and control. I'm going to walk you through the full workflow — from setting up a raise to researching investors, building a pipeline, writing outreach, prepping for due diligence, and writing investor updates. The whole thing. Let's go."

[TEXT OVERLAY] "Full workflow: onboard > research > pipeline > outreach > dd-prep > update"

---

### WALKTHROUGH (1:05 - 7:15)

#### Step 1: Onboard (1:05 - 2:15)

[SCREEN] Terminal. User types: `/investor:onboard synthwave`

[VO] "Starting from scratch. New fundraising workspace."

[SCREEN] INVESTOR:OS boot banner appears — the ASCII art, "Research it. Pitch it. Close it. Report it. by Shyft AI".

[VO] "INVESTOR:OS boots. Every OS in the ecosystem has its own identity. This one is purple. Because fundraising deserves its own mood."

[SCREEN] Role selection — user selects "Founder". Collaboration: "Solo". Execution mode:

```
  How should I handle approvals?

  >> Interactive — confirms each major decision
  >> Auto — auto-approves, only stops for hard gates:
     - Investor outreach (never auto-sends)
     - Term sheet responses
     - Data room sharing
     - Investor updates
```

User selects "Auto".

[VO] "Execution mode. I'm picking auto — which means it flies through internal work like research and pipeline management. But notice the hard gates. Investor outreach never auto-sends. Term sheet responses always stop. Data room sharing always stops. Investor updates always stop. The things that could blow up your raise — those always require your eyes."

[SCREEN] Round details:

```
  Round Setup

  Stage:          Seed
  Target raise:   $3M
  Valuation:      $12M pre (SAFE)
  Timeline:       4 months (June close target)
  Min check:      $100K
  Lead needed:    Yes
```

[VO] "Round setup. Stage, target, valuation, timeline. It uses seed-stage benchmarks — one to four million dollar raise, five to twenty investors, three to six month timeline — as defaults, and I adjust from there."

[SCREEN] Thesis building — each component asked separately:

```
  THESIS

  One-liner:   API monitoring that measures what users
               actually feel, not what dashboards show
  Problem:     Existing monitoring tools measure
               availability, not user experience
  Solution:    Real-user transaction monitoring with
               P95/P99 alerting
  Why now:     API-first architectures mean 10x more
               endpoints to monitor
  Traction:    $28K MRR, 140 companies, 3 enterprise
               pilots
  Moat:        Proprietary instrumentation layer, 2
               patents pending
```

[VO] "The thesis. Not a pitch deck — a structured argument. One-liner. Problem. Solution. Why now. Traction. Moat. Each component asked separately so you think clearly about each one. And this thesis feeds into everything else — outreach, deck prep, investor conversations."

[SCREEN] Workspace confirmation:

```
  Workspace created: /workspaces/synthwave/

  Files generated:
    THESIS.md      — investment thesis
    PIPELINE.md    — empty pipeline
    METRICS.md     — key metrics
    INVESTORS.md   — target list (empty)
    DATA-ROOM.md   — document checklist
    CAP-TABLE.md   — ownership structure
    MODEL.md       — financial model skeleton
    UPDATES.md     — investor update log
```

[VO] "Workspace created. Thesis, pipeline, metrics, data room checklist, cap table, financial model skeleton — all structured, all ready."

---

#### Step 2: Research (2:15 - 3:15)

[SCREEN] User types: `/investor:research synthwave "first-round-capital"`

[VO] "Now let's research an investor. First Round Capital. Let's see if they're a fit."

[SCREEN] Research begins:

```
  << INVESTOR:OS // RESEARCH >>

  Researching: First Round Capital
  Sources: Crunchbase, LinkedIn, recent interviews, blog posts...
```

[SCREEN] Research profile renders:

```
  FIRST ROUND CAPITAL

  Overview
    Stage focus:     Pre-seed, Seed
    Check size:      $1M - $5M (avg $2.5M)
    Sector focus:    Developer tools, SaaS, fintech
    Recent fund:     $650M (2024)
    Decision maker:  Partner — Bill Trenchard (dev tools)

  Portfolio (relevant)
    - Vercel (dev platform)
    - Snyk (security)
    - Notion (productivity)
    - Ramp (fintech)

  Thesis Alignment
    [x] Stage match    — Seed, check: $3M fits range
    [x] Sector match   — Developer tools: strong fit
    [x] Check size     — $2.5M avg, your ask is in range
    [ ] Portfolio conflict — NONE detected

  Warm Path Analysis
    - 2nd degree: Your advisor (Sarah Kim) invested
      alongside First Round in 2022
    - Content signal: Bill Trenchard tweeted about
      observability tooling 3 weeks ago

  Fit Score: 87/100 — STRONG MATCH

  Saved to INVESTORS.md
```

[VO] "Full research profile. Stage match, sector match, check size, portfolio companies. And look at this — warm path analysis. It found that my advisor co-invested with First Round two years ago. And the partner I'd want to talk to — Bill Trenchard — just tweeted about observability tooling. That's not a cold email. That's a warm intro with timing. Fit score: eighty-seven out of a hundred."

---

#### Step 3: Pipeline (3:15 - 3:55)

[SCREEN] User types: `/investor:pipeline synthwave`

[VO] "Let's look at the pipeline after adding a few more investors."

[SCREEN] Pipeline renders:

```
  << INVESTOR:OS // PIPELINE >>

  ┌─ INVESTOR PIPELINE ─────────────────────────────┐
  │                                                   │
  │  RESEARCHED (12)  ────────────────── 100%         │
  │  ██████████████████████████████████████████████   │
  │                                                   │
  │  CONTACTED (5)    ────────────────── 42%          │
  │  ███████████████████░░░░░░░░░░░░░░░░░░░░░░░░░░   │
  │                                                   │
  │  MEETING (3)      ────────────────── 25%          │
  │  ███████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
  │                                                   │
  │  DUE DILIGENCE (1) ──────────────── 8%            │
  │  ████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
  │                                                   │
  │  TERM SHEET (0)   ────────────────── 0%           │
  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
  │                                                   │
  │  CONVERSION RATES                                 │
  │  Researched → Contacted:  42%                     │
  │  Contacted → Meeting:     60%                     │
  │  Meeting → DD:            33%                     │
  │                                                   │
  │  STALE (no activity > 14 days)                    │
  │  - Sequoia — last contact: 18 days ago            │
  │  - Greylock — last contact: 21 days ago           │
  │                                                   │
  │  NEXT ACTIONS                                     │
  │  1. Follow up with Sequoia (stale 18d)            │
  │  2. Send deck to a16z (meeting scheduled Thu)     │
  │  3. First Round — intro request via Sarah Kim     │
  │                                                   │
  └───────────────────────────────────────────────────┘
```

[VO] "Pipeline funnel. Twelve researched, five contacted, three in meetings, one in diligence. Conversion rates at every stage. And stale conversations flagged — Sequoia hasn't heard from us in eighteen days. That's a follow-up I would have missed. Next actions are prioritized. This is how you run a raise — not with vibes, with a pipeline."

---

#### Step 4: Outreach (3:55 - 4:55)

[SCREEN] User types: `/investor:outreach synthwave "first-round-capital" --type warm`

[VO] "Let's draft outreach to First Round. Warm intro, through my advisor."

[SCREEN] Context loading:

```
  << INVESTOR:OS // OUTREACH >>

  Loading: THESIS.md, INVESTORS.md, METRICS.md
  Investor: First Round Capital (Bill Trenchard)
  Type: Warm intro request
  Warm path: Sarah Kim (advisor) → First Round
```

[SCREEN] Two emails render — the intro request and the forwardable email:

```
  ── EMAIL 1: Intro Request to Sarah Kim ──────────

  Subject: Quick intro ask — First Round / Bill Trenchard

  Hey Sarah,

  Quick ask. I saw Bill Trenchard at First Round tweeted
  about observability tooling a few weeks ago — which is
  basically what we're building at Synthwave.

  We're raising a $3M seed. $28K MRR, 140 companies on
  the platform, 3 enterprise pilots closing this quarter.

  Would you be open to making an intro? I've drafted a
  forwardable below so it's zero effort on your end.

  Thanks,
  [Founder]


  ── EMAIL 2: Forwardable to Bill Trenchard ───────

  Subject: Synthwave — API monitoring for what users
  actually feel

  Bill,

  {Sarah's name} suggested I reach out. We're building
  Synthwave — API monitoring that measures real user
  experience, not just uptime dashboards.

  Quick context:
  - $28K MRR, growing 22% MoM
  - 140 developer teams on the platform
  - 3 enterprise pilots (2 converting this month)
  - Raising $3M seed, $12M pre-money SAFE

  Your thesis around developer infrastructure and your
  portfolio (Vercel, Snyk) are exactly the ecosystem
  we're building for.

  Would love 20 minutes to walk you through the product
  and what we're seeing in the market.

  [Founder]

  ──────────────────────────────────────────────────

  !! HARD GATE — INVESTOR OUTREACH !!
  Review both emails carefully before sending.

  >> Approve / Edit / Cancel
```

[VO] "Two emails. The intro request to Sarah — easy, specific, with context on why Bill is the right person. And the forwardable — the email Sarah can just forward with no effort. Notice what's in the forwardable: traction first, not product description. Specific numbers. Portfolio overlap — Vercel, Snyk. And a clear ask — twenty minutes. Not 'I'd love to connect sometime.' And right there — the hard gate. Even in auto mode, this stops. Because investor outreach is too important to auto-send. You review. You edit. You approve."

[SCREEN] User types: `approve`

```
  Outreach saved: outreach/first-round-capital.md
  Pipeline updated: First Round → CONTACTED
  Follow-up scheduled: 5 business days
```

[VO] "Approved. Saved. Pipeline updated automatically. Follow-up reminder set for five days."

---

#### Step 5: DD Prep (4:55 - 5:55)

[SCREEN] User types: `/investor:dd-prep synthwave`

[VO] "Now let's say a conversation goes well and an investor wants to do due diligence. This command gets you ready before they ask."

[SCREEN] DD checklist renders:

```
  << INVESTOR:OS // DD PREP >>

  DUE DILIGENCE READINESS

  CORPORATE
    [x] Certificate of incorporation
    [x] Bylaws / operating agreement
    [ ] Board minutes                    !! MISSING
    [ ] Cap table (fully diluted)        !! NEEDS UPDATE

  FINANCIAL
    [x] P&L — last 12 months
    [x] Bank statements
    [x] Revenue by customer (top 10)
    [ ] Financial projections (3yr)      !! MISSING
    [ ] Unit economics breakdown         !! MISSING

  LEGAL
    [x] IP assignment agreements
    [x] Employee agreements
    [ ] Material contracts               !! 2 unsigned
    [ ] Privacy policy / ToS review      !! NEEDS UPDATE

  PRODUCT
    [x] Product roadmap
    [x] Technical architecture doc
    [x] Security practices overview

  COMMERCIAL
    [x] Customer list with ARR
    [ ] Churn analysis                   !! MISSING
    [x] Pipeline summary

  READINESS SCORE: 64% (9 of 14 items ready)

  RED FLAGS TO ADDRESS PROACTIVELY
    1. Board minutes — create retroactively for
       quarterly decisions
    2. Cap table — update with advisor grants and
       SAFE conversions
    3. 2 unsigned contracts — get these signed this week

  REMEDIATION TIMELINE
    Week 1: Board minutes, contract signatures
    Week 2: Cap table update, financial projections
    Week 3: Unit economics, churn analysis, privacy review
    Week 4: Final review — target 100% readiness
```

[VO] "Due diligence readiness. Fourteen items across five categories. Nine ready, five missing. And it doesn't just tell you what's missing — it tells you what to do about it. Board minutes need to be created retroactively. Two contracts are unsigned. Cap table needs updating. And it gives you a remediation timeline. Four weeks to get from sixty-four percent to one hundred percent ready. The worst thing in a fundraise is scrambling for documents when an investor asks. This means you're ready before they even ask the question."

---

#### Step 6: Investor Update (5:55 - 6:45)

[SCREEN] User types: `/investor:update synthwave --type monthly`

[VO] "Last thing. Investor updates. The task every founder dreads and every investor wishes you'd do more."

[SCREEN] Update renders:

```
  << INVESTOR:OS // UPDATE >>

  Loading: METRICS.md, UPDATES.md, ROADMAP.md

  ── MONTHLY INVESTOR UPDATE — MARCH 2026 ────────

  HIGHLIGHTS
    - Crossed $35K MRR (up 25% MoM)
    - Signed first enterprise contract ($48K ACV)
    - Hired Head of Engineering (ex-Datadog)

  METRICS
  | Metric      | Mar     | Feb     | Delta  |
  |-------------|---------|---------|--------|
  | MRR         | $35,100 | $28,000 | +25%   |
  | Customers   | 156     | 140     | +11%   |
  | NRR         | 118%    | 112%    | +6pts  |
  | Burn        | $95K    | $92K    | +3.3%  |
  | Runway      | 8.2 mo  | 9.1 mo  | -0.9   |

  KEY WINS
    - Enterprise: Closed first $48K ACV deal (12-mo)
    - Product: Launched real-user monitoring (RUM) beta
    - Team: Head of Eng start date April 7

  CHALLENGES (being honest)
    - Sales cycle for enterprise: 47 days avg (target: 30)
    - Need senior frontend engineer — still searching
    - Burn increasing faster than planned due to
      infrastructure costs

  ASKS (be specific)
    1. Intro to VP Engineering at Stripe — exploring
       design partnership for payment flow monitoring
    2. Recommendations for fractional CFO for Series A
       prep
    3. Feedback on updated deck (attached)

  NEXT MONTH FOCUS
    - Close 2 more enterprise pilots
    - Ship RUM GA
    - Begin Series A positioning

  ──────────────────────────────────────────────────

  !! HARD GATE — INVESTOR UPDATE !!
  Review carefully. This goes to your investors.

  >> Approve / Edit / Cancel
```

[VO] "Structured update. Highlights — the wins. Metrics table — current, previous, delta. Honest challenges — not just the good stuff. And look at the asks — specific, actionable. Not 'let me know if you can help.' An intro to a specific person at a specific company for a specific reason. That's how you get value from your investors. And again — hard gate. Even in auto mode. Because this goes to real investors with real reputations and real checkbooks. You review every word."

---

#### Step 7: FOUNDER:OS Connection (6:45 - 7:15)

[SCREEN] Quick cut to a different terminal. User types: `/founder:today`

[VO] "One more thing. FOUNDER:OS — the meta layer. When I run my daily cockpit..."

[SCREEN] FOUNDER:OS cockpit loads. The FUNDRAISE section highlights:

```
  FUNDRAISE                           via INVESTOR:OS
    Pipeline: 12 investors | 3 meetings | 1 in DD
    Next: Partner meeting at a16z (Thursday)
    Action: Follow up with Sequoia (18d stale)
    Update: March update sent to 4 investors
```

[VO] "My fundraise status flows right into my daily founder cockpit. Pipeline stage. Next meeting. Stale follow-ups. All pulled live from INVESTOR:OS. I never have to context-switch into fundraise mode — it's already in my morning briefing."

---

### RESULTS RECAP (7:15 - 7:45)

[SCREEN] Summary card:

```
  SESSION RECAP

  1. Workspace created    — thesis, pipeline, data room
  2. Investor researched  — deep profile, fit score 87/100
  3. Pipeline managed     — 12 investors, conversion tracked
  4. Outreach drafted     — warm intro, forwardable email
  5. DD prep complete     — 64% ready, remediation plan
  6. Update written       — structured, honest, specific asks
  7. Cockpit connected    — fundraise in daily briefing

  Hard gates respected: outreach, update (2 stops)
  Everything else: auto-executed
```

[VO] "Full fundraising workflow. From thesis to pipeline to outreach to diligence to investor updates. Pipeline managed like actual pipeline — with stages, conversion rates, and stale warnings. Outreach personalized with portfolio overlap and warm paths. Due diligence prepped before anyone asks. Updates structured with honest challenges and specific asks. And hard gates on everything investor-facing. Fundraising is a sales process. Now it has a sales system."

---

### CTA (7:45 - 8:00)

[SCREEN] Terminal. INVESTOR:OS banner visible.

```
  github.com/shyftai

  Clone it. Run /investor:onboard. Your pipeline in 10 minutes.
```

[TEXT OVERLAY] "INVESTOR:OS — free and open source"

[VO] "INVESTOR:OS is free and open source. Clone it, run /investor:onboard, and have your fundraise structured in ten minutes. Next video — I'm showing you how AUTO mode makes everything ten times faster without losing the guardrails. Subscribe so you don't miss it."

---

---

## Script 6: "How AUTO Mode 10x'd My Execution Speed"

**Total runtime:** ~6 minutes

---

### TITLE CARD (0:00 - 0:05)

[SCREEN] Black background. Text fades in:

```
AUTO MODE
How I 10x'd My Execution Speed

Antigravity OS by Shyft AI
```

[TEXT OVERLAY] Small Shyft AI logo, bottom right.

---

### HOOK (0:05 - 0:30)

[SCREEN] Terminal. Quick montage of approval gates popping up — "Approve? (approve / edit / reject)" — one after another. Four in a row. User typing "approve" each time. Feels tedious.

[VO] "The biggest complaint with AI tools is the constant 'are you sure?' prompts. Every step. Every decision. 'Do you want me to continue?' Yes. 'Should I save this?' Yes. 'Can I proceed?' YES. You spend more time approving than actually working. I got so frustrated with this that I built a mode that eliminates the noise. But keeps the guardrails where you actually need them."

[TEXT OVERLAY] "Less 'are you sure?' More 'it's done.'"

---

### CONTEXT (0:30 - 0:55)

[SCREEN] Terminal. `workspace.config.md` file visible in the editor:

```
  **Execution mode:** interactive
```

[VO] "Every workspace in the Antigravity ecosystem has an execution mode. Interactive is the default — it stops and asks at every decision point. It's safe. It's thorough. And for some workflows, it's exactly right. But for the stuff you do every day? The copy you're going to approve anyway? The validation you just need to run? It's friction. AUTO mode fixes that. Let me show you the difference."

---

### WALKTHROUGH (0:55 - 5:15)

#### Part 1: Interactive Mode (0:55 - 2:15)

[SCREEN] Terminal. User types: `/gtm:write acme`

[TEXT OVERLAY] "INTERACTIVE MODE"

[VO] "Interactive mode first. I'm writing a cold email sequence in GTM:OS."

[SCREEN] GTM:OS banner appears. Context loads:

```
  Loading workspace context...
    ICP: loaded
    Persona: loaded
    TOV: loaded
    Campaign learnings: loaded
    Suppression list: checked
```

[VO] "Context loads. All good."

[SCREEN] First approval gate appears:

```
  Campaign brief generated.

  Target: VP Engineering at Series A-C SaaS
  Angle: Developer productivity
  Touches: 4
  Tone: Direct, technical, peer-level

  >> Approve brief? (approve / edit / reject)
```

User types: `approve`

[VO] "First gate. Campaign brief. Looks fine. Approve."

[SCREEN] Sequence drafts. Then second gate:

```
  Touch 1 drafted.

  Subject: {{company}} + API response times
  Body: [3-line email visible]

  >> Approve touch 1? (approve / edit / reject)
```

User types: `approve`

[VO] "Second gate. Touch 1. Looks good. Approve."

[SCREEN] Third gate:

```
  Touches 2-4 drafted.

  Touch 2: Value nudge (case study angle)
  Touch 3: Direct ask (breakup)
  Touch 4: Resurface (trigger event)

  >> Approve remaining touches? (approve / edit / reject)
```

User types: `approve`

[VO] "Third gate. Remaining touches. Approve."

[SCREEN] Quality gates run. Fourth gate:

```
  QUALITY GATES
    [x] Brief alignment
    [x] No invented URLs
    [x] No fake merge fields
    [x] Tone of voice
    [x] Spam word check
    [x] CTA clarity
    [x] Readability

  >> Save to copy/approved/? (approve / edit / reject)
```

User types: `approve`

[VO] "Fourth gate. Quality check. All green. Save. Four approvals for one write command. Each one taking ten seconds of 'let me read, okay, approve.' That's forty seconds of friction. Multiply that across every command, every day."

[SCREEN] Timer appears in corner: "Total approval time: ~40 seconds" with a subtle red tint.

---

#### Part 2: Switch to AUTO (2:15 - 2:35)

[SCREEN] User opens workspace.config.md in the editor. Changes:

```
  **Execution mode:** interactive
```

to:

```
  **Execution mode:** auto
```

[VO] "One line change. That's it."

[TEXT OVERLAY] "workspace.config.md — one line"

[VO] "You can also just say 'switch to auto' mid-session. But I want you to see where it lives. One line in your workspace config. Now watch what happens."

---

#### Part 3: AUTO Mode (2:35 - 3:55)

[SCREEN] Terminal. User types: `/gtm:write acme`

[TEXT OVERLAY] "AUTO MODE" with a lightning bolt icon

[VO] "Same command. Same workspace. AUTO mode."

[SCREEN] GTM:OS banner appears. Context loads. Then — no gates. Everything flows:

```
  Loading workspace context...
    ICP: loaded
    Persona: loaded
    TOV: loaded
    Campaign learnings: loaded
    Suppression list: checked

  ⚡ Auto-approved: campaign brief (VP Eng, Series A-C, dev productivity)

  Drafting sequence...

  ⚡ Auto-approved: Touch 1 — cold open (API response times)
  ⚡ Auto-approved: Touch 2 — value nudge (case study)
  ⚡ Auto-approved: Touch 3 — breakup (direct ask)
  ⚡ Auto-approved: Touch 4 — resurface (trigger event)

  QUALITY GATES
    [x] Brief alignment
    [x] No invented URLs
    [x] No fake merge fields
    [x] Tone of voice
    [x] Spam word check
    [x] CTA clarity
    [x] Readability

  ⚡ Auto-approved: saved to copy/approved/campaign-vp-eng-dev-productivity.md

  Logged: 5 auto-approvals → logs/decisions.md

  Done. 4-touch sequence ready. /gtm:ship when ready to send.
```

[VO] "Watch it fly. Context loaded. Brief auto-approved with a one-liner so you can see what it chose. Touches drafted and auto-approved — each one logged. Quality gates run — all green. Saved. Five auto-approvals, each one logged to a decisions file so you have a full audit trail. And it's done. Same output. Zero friction. The sequence is sitting in copy/approved, ready to go."

[SCREEN] Timer: "Total approval time: 0 seconds" with a green tint. Side by side with the previous "40 seconds".

[VO] "Zero seconds of approval time. Same quality output. All approvals logged."

---

#### Part 4: The Hard Gates (3:55 - 5:15)

[SCREEN] Terminal. User types: `/gtm:ship acme`

[TEXT OVERLAY] "But here's the important part..."

[VO] "But here's the important part. Watch what happens when I try to ship."

[SCREEN] GTM:OS loads. Ship sequence begins:

```
  << GTM:OS // SHIP >>

  Loading campaign: vp-eng-dev-productivity
  Checking prerequisites...

  Pre-flight checks:
    [x] Copy approved
    [x] List validated
    [x] Suppression list checked (847 contacts)
    [x] Sending tool connected (Smartlead)
    [x] Credits available (est. 247 sends × $0.02)
    [x] No compliance violations
    [x] Sending window: Mon-Thu, 8-11am recipient TZ
    [x] No holiday blackouts

  ─────────────────────────────────────────────────
  !! HARD GATE — LAUNCH APPROVAL !!

  This will push 247 contacts into Smartlead
  and begin sending tomorrow at 8:00am ET.

  Estimated cost: $4.94
  Campaign: vp-eng-dev-productivity
  Touches: 4 (spaced 3-5 days)

  THIS CANNOT BE UNDONE ONCE SENDING BEGINS.

  >> APPROVE TO SHIP? (approve / cancel)
  ─────────────────────────────────────────────────
```

[VO] "Everything ran automatically — pre-flight checks, suppression list, compliance, sending window, holiday blackouts. All auto-approved. And then — full stop. Hard gate. Even in AUTO mode. 'This will push 247 contacts into Smartlead and begin sending tomorrow. This cannot be undone once sending begins.' You have to type approve. There is no auto for this."

[SCREEN] User types: `approve`

```
  Campaign pushed to Smartlead.
  247 contacts loaded.
  Sending begins: March 11, 8:00am ET.

  Monitor: /gtm:today for delivery stats
```

[VO] "Now I approve because I've seen the numbers, I've seen the copy, I trust the system. But the system made me look."

[CUT TO] Quick montage of hard gates from other frameworks:

[SCREEN] CS:OS:

```
  !! HARD GATE — CONTRACT CHANGES !!
  This renewal modifies contract terms.
  >> Approve changes? (approve / edit / cancel)
```

[SCREEN] INVESTOR:OS:

```
  !! HARD GATE — INVESTOR OUTREACH !!
  Review both emails carefully before sending.
  >> Approve / Edit / Cancel
```

[SCREEN] HR:OS:

```
  !! HARD GATE — OFFER LETTER !!
  Offers must never be sent without explicit sign-off.
  >> Approve / Edit / Cancel
```

[SCREEN] INVESTOR:OS:

```
  !! HARD GATE — INVESTOR UPDATE !!
  This goes to your investors. Review carefully.
  >> Approve / Edit / Cancel
```

[VO] "Every framework has them. CS:OS stops on contract changes. INVESTOR:OS stops on outreach and updates. HR:OS stops on offer letters and PIPs. These are the decisions where a mistake costs you real money, real relationships, or real legal exposure. AUTO mode trusts you on the small decisions so you can focus on the ones that matter."

---

### RESULTS RECAP (5:15 - 5:45)

[SCREEN] Side-by-side comparison card:

```
  INTERACTIVE vs AUTO

  Same /gtm:write command

  INTERACTIVE                   AUTO
  ──────────────────────────────────────────
  4 approval gates              0 approval gates
  ~40 sec of friction           0 sec of friction
  Same output quality           Same output quality
  No audit trail                Full audit trail
                                (logs/decisions.md)

  HARD GATES
  ──────────────────────────────────────────
  /gtm:ship                    ALWAYS stops
  Contract changes (CS:OS)     ALWAYS stops
  Investor outreach            ALWAYS stops
  Offer letters (HR:OS)        ALWAYS stops
  PIPs (HR:OS)                 ALWAYS stops
  Budget overages              ALWAYS stops
  Compliance violations        ALWAYS stops

  AUTO mode: trust the system on the 95%.
  Stay sharp on the 5% that matters.
```

[VO] "Same command. Same output. Zero friction on the routine stuff. Full stop on the stuff that matters. And here's the thing people miss — AUTO mode actually gives you a better audit trail than interactive mode. Every auto-approval is logged with a timestamp and what was approved. In interactive mode, you just typed 'approve' and moved on. No record. AUTO mode documents everything."

---

### CTA (5:45 - 6:00)

[SCREEN] Terminal. All eight OS banners flash in quick succession — orange, blue, green, coral, violet, teal, cyan, gold.

```
  github.com/shyftai

  Every OS supports AUTO mode. Clone any of them.
  Run /[prefix]:onboard. Set execution mode to auto.
```

[TEXT OVERLAY] "Antigravity OS — free and open source"

[VO] "Every OS in the Antigravity ecosystem supports AUTO mode. Clone any of them. Run onboard. Set your execution mode to auto. And watch your speed change. All free. All open source. Subscribe for more — next video I'm showing you how the swarm mode runs twenty campaigns in parallel. Link in the description."

---

---

## Production Notes

### Recording Setup
- **Resolution:** 1920x1080 landscape (YouTube standard)
- **Terminal theme:** Dark (Dracula or One Dark) — must match across all scripts
- **Font size:** 16-18pt for readability at 1080p (larger than shorts — viewers are on desktop)
- **Editor:** VS Code with minimal UI — hide activity bar, keep sidebar collapsed unless showing file structure
- **Terminal width:** At least 80 columns for the ASCII art banners to render cleanly
- **Typing:** Type live for authenticity. Reasonable speed — not too fast, not hunt-and-peck. Slight pauses before hitting Enter (builds anticipation)

### Voiceover Style
- **Tone:** Founder explaining to a friend. Passionate but not performative
- **Pacing:** Slightly faster than conversational during walkthroughs. Slow down for key insights and hard gate explanations
- **Energy:** Build momentum during AUTO mode comparisons. Drop to serious for hard gate explanations
- **No filler:** Cut "um", "uh", "basically" in editing. But don't make it sound scripted — a few natural pauses are fine
- **Record separately from screen:** Voiceover layered in post, not live-narrated. This lets you speed up terminal rendering without speeding up the voice

### Editing Guidance
- **Terminal output:** Speed up rendering to 2-3x where text is flowing (viewers can pause if they want to read). Normal speed when the user is typing commands
- **Transitions:** Hard cuts between sections. No dissolves, no wipes. One exception: the title card can fade in
- **Zooms:** Subtle 110-120% zoom on key numbers (MRR, fit scores, pipeline counts, hard gate warnings). Don't overdo it — two or three per video max
- **Split screens:** Use for the AUTO mode comparison in Script 6. Left = interactive with red tint, right = auto with green tint
- **Text overlays:** Bold sans-serif (Inter or similar). White text with subtle dark shadow. Bottom third positioning. Hold for 3-4 seconds minimum — these are longer videos, viewers need time to read
- **Music:** Light ambient/electronic during title card and CTA only. Silence during demo sections — the terminal sounds (if any) and voice are enough. For Script 6, consider a subtle tempo increase during the AUTO mode section
- **B-roll:** Minimal. The terminal IS the content. Quick cuts to browser/sheets/email are fine for hooks (showing the "before" state)
- **End cards:** YouTube end screen with subscribe button and next video thumbnail. Leave 15 seconds of clean space at the end for the overlay

### Thumbnail Suggestions

**Script 4 (Content Engine):**
- Terminal screenshot showing "4 pieces of content from 1 article" with a calendar grid visible
- Text: "CONTENT ENGINE" in bold
- Founder pointing at screen (if using face-cam thumbnails)

**Script 5 (Fundraising):**
- Terminal screenshot showing the pipeline funnel with conversion percentages
- Text: "FUNDRAISE LIKE A PIPELINE"
- Red/orange urgency color scheme

**Script 6 (AUTO Mode):**
- Split screen thumbnail — left side shows 4 approval prompts (red), right side shows lightning bolts (green)
- Text: "AUTO MODE" with "10x FASTER" below
- Lightning bolt icon

### Series Consistency
- Same terminal theme across all three videos
- Same text overlay font and positioning
- Same intro sound/music sting (if using one)
- End each video by teasing the next one in the series
- Add chapter markers in YouTube descriptions matching the timestamp sections in these scripts
