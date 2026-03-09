# FOUNDER:OS — The Founder Operating System

> See everything. Decide fast. Move forward.

FOUNDER:OS is a Claude Code plugin that gives founders a single cockpit across their entire business. It connects to domain-specific OS frameworks (GTM:OS, CONTENT:OS, FINANCE:OS, HR:OS, INVESTOR:OS, COMMUNITY:OS) and pulls live data into unified dashboards, decision frameworks, and board-ready reports.

**Built for:** founders, CEOs, co-founders, and COOs running early-to-growth-stage companies.

---

## Install

### Prerequisites
You need [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed:
```
npm install -g @anthropic-ai/claude-code
```

### Get started
```
git clone https://github.com/shyftai/FOUNDEROS.git
cd FOUNDEROS
claude
```

That's it. FOUNDER:OS boots automatically — shows the banner, detects your connected OS frameworks, and asks which workspace to load. No config files to edit, no build step.

### Connect your OS frameworks
FOUNDER:OS reads data from other OS frameworks in the Antigravity ecosystem. Install any of these alongside FOUNDER:OS:

| Framework | What it covers | Repo |
|-----------|---------------|------|
| **GTM:OS** | Pipeline, outbound, campaigns | `/c/Antigravity/GTMOS` |
| **CONTENT:OS** | Content strategy, publishing | `/c/Antigravity/CONTENTOS` |
| **FINANCE:OS** | Runway, burn, invoicing, budget | `/c/Antigravity/FINANCEOS` |
| **HR:OS** | Hiring, team, culture, performance | `/c/Antigravity/HROS` |
| **INVESTOR:OS** | Fundraising, investor relations | `/c/Antigravity/INVESTOROS` |
| **COMMUNITY:OS** | Community building, engagement | `/c/Antigravity/COMMUNITYOS` |

You don't need all frameworks to start. FOUNDER:OS works with whatever you have and tells you what's connected.

### First run
When FOUNDER:OS boots, run:
```
/founder:onboard my-company
```
It asks your role, walks you through company setup, detects connected frameworks, and creates your workspace. Then you're ready to run your business from one place.

---

## What it looks like

### Boot sequence
```
███████╗ ██████╗ ██╗   ██╗███╗   ██╗██████╗ ███████╗██████╗  ██╗  ██████╗ ███████╗
██╔════╝██╔═══██╗██║   ██║████╗  ██║██╔══██╗██╔════╝██╔══██╗ ╚═╝ ██╔═══██╗██╔════╝
█████╗  ██║   ██║██║   ██║██╔██╗ ██║██║  ██║█████╗  ██████╔╝     ██║   ██║███████╗
██╔══╝  ██║   ██║██║   ██║██║╚██╗██║██║  ██║██╔══╝  ██╔══██╗ ██╗ ██║   ██║╚════██║
██║     ╚██████╔╝╚██████╔╝██║ ╚████║██████╔╝███████╗██║  ██║ ╚═╝ ╚██████╔╝███████║
╚═╝      ╚═════╝  ╚═════╝ ╚═╝  ╚═══╝╚═════╝ ╚══════╝╚═╝  ╚═╝     ╚═════╝ ╚══════╝
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  F O U N D E R : O S                                                        v1.0.0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  See everything. Decide fast. Move forward.

  ┌─ SYSTEM ──────────────────────────────────────────────────┐
  │                                                            │
  │  Connected OS frameworks:                                  │
  │  [x] GTM:OS        [x] CONTENT:OS     [x] FINANCE:OS      │
  │  [x] HR:OS         [x] INVESTOR:OS    [x] COMMUNITY:OS    │
  │                                                            │
  │  Workspaces:  acme-corp                                    │
  │  Mode:        solo                                         │
  │  Execution:   interactive                                  │
  │                                                            │
  │  6 frameworks · 0 MCP servers · 0 API keys                 │
  │                                                            │
  └────────────────────────────────────────────────────────────┘

  >> Which workspace are we loading?
```

### Daily cockpit
```
  << FOUNDER:OS // TODAY >>

  ┌─ COMPANY PULSE ──────────────────────────────────┐
  │                                                    │
  │  GTM:OS        Pipeline: $1.2M  Meetings: 3 today │
  │  FINANCE:OS    Runway: 14mo     Burn: $42K/mo      │
  │  HR:OS         Open roles: 2    Offers: 1 pending  │
  │  INVESTOR:OS   Pipeline: 4      Follow-ups: 2 due  │
  │  CONTENT:OS    Due today: 1     Published: 12/wk   │
  │  COMMUNITY:OS  Members: 847     Engage: 8.2%       │
  │                                                    │
  │  OKRs: 2 on track, 1 at risk                      │
  │  Decisions pending: 2                              │
  │  Energy: Deep work block until 11am                │
  │                                                    │
  └────────────────────────────────────────────────────┘

  Top 3 actions for today:
  1. Review Series A term sheet (INVESTOR:OS — Type 1 decision)
  2. Approve Q2 content calendar (CONTENT:OS — Type 2, delegate)
  3. Prep for board meeting Thursday (FOUNDER:OS — board-update)
```

### Decision framework
```
  ┌─ DECISION ──────────────────────────────────────┐
  │                                                  │
  │  "Should we expand to the EU market?"            │
  │                                                  │
  │  Type:    1 (irreversible — market commitment)   │
  │  OKR:     Revenue growth +40% (KR2)             │
  │  Data:    EU pipeline $340K, 23 qualified leads   │
  │  Risk:    GDPR compliance, 2-month setup          │
  │                                                  │
  │  ── DECISION GATES ───────────────────────────   │
  │  [x] Vision       [x] OKR impact                │
  │  [x] Data backed  [ ] Reversible                 │
  │  [x] Delegation   [~] Energy                     │
  │  ─────────────────────────────────────────────   │
  │                                                  │
  │  Recommendation: Proceed with phased approach    │
  │  Review date: 2024-04-15                         │
  │                                                  │
  └──────────────────────────────────────────────────┘
  >> Approve / Reject / Defer / Need more data
```

### Board update
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  BOARD UPDATE — Q1 2024                                     ┃
┃  HARD GATE: Requires explicit approval before sending       ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                                                             ┃
┃  Highlights                                                 ┃
┃  - Revenue: $128K MRR (+22% QoQ)                           ┃
┃  - Pipeline: $1.2M weighted                                ┃
┃  - Team: 12 → 15 (3 hires closed)                         ┃
┃  - Runway: 14 months at current burn                       ┃
┃                                                             ┃
┃  Key Metrics                                                ┃
┃  [pulled from GTM:OS, FINANCE:OS, HR:OS, COMMUNITY:OS]    ┃
┃                                                             ┃
┃  Challenges                                                 ┃
┃  - Enterprise sales cycle longer than forecast              ┃
┃  - Senior engineer search: 8 weeks, no close               ┃
┃                                                             ┃
┃  Asks                                                       ┃
┃  - Board intro to [Target Company] CTO                     ┃
┃                                                             ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
  >> Approve / Edit / Reject
```

---

## How it works

```
  ┌──────────────────────────────────────────────────────────┐
  │                                                          │
  │  VISION ─── OKRs ─── PRIORITIES                          │
  │                 │                                        │
  │            DELEGATION                                    │
  │                 │                                        │
  │    ┌────────────┼────────────┐                           │
  │    ▼            ▼            ▼                           │
  │  GTM:OS    FINANCE:OS    HR:OS                           │
  │  CONTENT:OS INVESTOR:OS COMMUNITY:OS                     │
  │    │            │            │                           │
  │    ▼            ▼            ▼                           │
  │  METRICS ── DECISIONS ── LEARN                           │
  │                 │                                        │
  │          WEEKLY REVIEW                                   │
  │                 │                                        │
  │       BOARD UPDATE / REPORT                              │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

Every decision is checked against six gates before proceeding:

| Gate | What it checks |
|------|---------------|
| **Vision alignment** | Does this serve the company vision? |
| **OKR impact** | Which key result does this move? |
| **Data backing** | What do the numbers say? |
| **Reversibility** | Type 1 (irreversible) or Type 2 (reversible)? |
| **Delegation** | Should someone else decide this? |
| **Energy** | Is this the best use of founder time? |

If it doesn't pass the gates, it doesn't proceed.

---

## The founder's workflow

**1. Morning cockpit** → `/founder:today` shows everything that matters right now. Pulled live from all connected OS frameworks. Priorities, decisions pending, metrics at a glance.

**2. Make decisions** → `/founder:decide` walks through structured frameworks. Type 1 decisions get deep analysis. Type 2 decisions get speed. Everything logged in DECISIONS.md.

**3. Delegate work** → `/founder:delegate` routes tasks to the right OS framework or team member. Track delegation in DELEGATION.md.

**4. Weekly review** → `/founder:weekly` pulls the week's data from all frameworks. Wins, misses, learnings, next week's priorities. Feeds into LEARNINGS.md.

**5. Board and investors** → `/founder:board-update` and `/founder:investor-update` generate communications from real data. Always a hard gate — requires approval before sending.

**6. Strategy sessions** → `/founder:strategy` for quarterly planning, `/founder:okrs` for OKR management, `/founder:pivot` for structured pivot analysis.

---

## All commands

### Cockpit
| Command | What it does |
|---------|-------------|
| `/founder:today` | Daily cockpit — pulls from ALL frameworks |
| `/founder:dashboard` | Full company overview across all OS |
| `/founder:weekly` | Weekly review — wins, misses, next week |
| `/founder:metrics` | North star + key metrics across all OS |

### Strategy
| Command | What it does |
|---------|-------------|
| `/founder:vision` | Define/refine company vision |
| `/founder:okrs` | Set, track, review OKRs |
| `/founder:priorities` | Manage top 3 priorities |
| `/founder:strategy` | Strategic planning — quarterly, annual |
| `/founder:pivot` | Structured pivot analysis |

### Decide
| Command | What it does |
|---------|-------------|
| `/founder:decide` | Structured decision framework |
| `/founder:delegate` | Assign work to people/frameworks |
| `/founder:risks` | Risk register — what could go wrong |
| `/founder:launch` | Product/campaign launch checklist |

### People
| Command | What it does |
|---------|-------------|
| `/founder:hire` | Hiring decision framework (routes to HR:OS) |
| `/founder:network` | Manage advisor/mentor relationships |
| `/founder:energy` | Manage founder energy and deep work |

### Money
| Command | What it does |
|---------|-------------|
| `/founder:fundraise` | Fundraising decisions (routes to INVESTOR:OS) |
| `/founder:board-update` | Generate board update from all OS data |
| `/founder:investor-update` | Generate investor update from all OS data |

### Review
| Command | What it does |
|---------|-------------|
| `/founder:review` | Monthly/quarterly business review |
| `/founder:debrief` | Retrospective on a quarter/initiative |
| `/founder:report` | Company performance report |

### More
| Command | What it does |
|---------|-------------|
| `/founder:onboard` | Set up founder workspace |
| `/founder:switch` | Switch workspace |
| `/founder:status` | Show all commands and system status |
| `/founder:feedback` | Report a bug or request a feature |

---

## Repo structure

```
FOUNDEROS/
├── CLAUDE.md                  <- Entrypoint for Claude Code
├── FOUNDEROS.md               <- All rules and behaviour
├── CHANGELOG.md               <- Version history
├── .env.example               <- API key template
├── _template/                 <- Workspace template (copied on onboard)
├── global/                    <- Cross-workspace standards
│   ├── RULES-GLOBAL.md        <- Global quality rules
│   └── COLLABORATION.md       <- Solo/team mode config
├── .claude/
│   ├── commands/founder/      <- Slash commands (/founder:*)
│   └── founderos/references/  <- System references
│       ├── decision-frameworks.md  <- RAPID, Type 1/2, 70% rule
│       ├── okr-guide.md           <- OKR writing and scoring
│       ├── board-guide.md         <- Board meeting prep and updates
│       ├── energy-management.md   <- Deep work, maker schedule
│       ├── BENCHMARKS.md          <- Startup benchmarks by stage
│       ├── defaults.md            <- All overridable defaults
│       ├── report-template.md     <- Report formats
│       ├── notifications.md       <- Slack alert config
│       ├── tool-pricing.md        <- Per-unit costs
│       └── ui-brand.md            <- Visual patterns
└── workspaces/                <- One folder per company
```

---

## Feedback

Found a bug? Want a feature? Run `/founder:feedback` inside Claude Code, or open an issue on this repo.

---

## License

MIT — Built by [Shyft AI](https://shyft.ai)
