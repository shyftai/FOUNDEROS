# FOUNDER:OS Swarm Architecture

Parallel agent execution for executive operations. Use when a task spans multiple business functions, departments, or strategic analyses.

---

## When to Swarm

| Scenario | Agents | Why Parallel |
|----------|--------|-------------|
| Cross-OS health check | 1 per OS framework | Each framework is independent |
| Strategic planning (multi-department) | 1 per department | Each department's input is standalone |
| Board meeting prep | 1 per section | Financials, product, go-to-market — parallel |
| OKR review (company-wide) | 1 per team | Each team's OKR progress is independent |
| Due diligence response | 1 per workstream | Legal, financial, technical — parallel tracks |
| Competitive landscape | 1 per competitor | Each competitor is standalone research |

---

## Agent Types

| Color | Role | Typical Task |
|-------|------|-------------|
| **magenta** | Research | Market research, competitive intelligence, industry trends |
| **cyan** | Planning / Verification | OKR verification, strategic plan review, assumption testing |
| **green** | Execution | Report generation, presentation building, communication drafting |
| **red** | Risk / Issues | Risk assessment, scenario analysis, crisis evaluation |
| **yellow** | Strategy / Synthesis | Cross-functional synthesis, board material, strategic recommendations |
| **blue** | Integration | Cross-OS data collection, dashboard aggregation, tool health checks |

---

## Batch Sizing

| Operation | Max per Agent | Reason |
|-----------|--------------|--------|
| OS framework health check | 2 frameworks | Each needs thorough review |
| Competitor analysis | 1 competitor | Deep analysis requires focus |
| Department OKR review | 1 department | Context-specific scoring |
| Board section preparation | 1 section | Quality over speed |
| Strategic initiative review | 3 initiatives | Higher-level pattern matching |
| Hiring pipeline review | 1 department | Each has unique requirements |

---

## Wave Structure

### Example: Quarterly Strategic Review

```
Wave 1: Data Collection (parallel)
  → blue Integration: pull metrics from FINANCE:OS
  → blue Integration: pull metrics from GTM:OS
  → blue Integration: pull metrics from PRODUCT:OS
  → blue Integration: pull metrics from HR:OS

Wave 2: Analysis (parallel, depends on Wave 1)
  → yellow Strategy: revenue and growth analysis
  → yellow Strategy: product and engineering velocity
  → yellow Strategy: team health and capacity
  → magenta Research: market and competitive position

Wave 3: Synthesis (depends on Wave 2)
  → yellow Strategy: quarterly strategic review document
  → cyan Planning: next quarter priorities and OKRs
  → red Risk: risk register update
```

### Example: Board Meeting Prep

```
Wave 1: Section Drafting (parallel)
  → green Execution: financial overview section
  → green Execution: product milestones section
  → green Execution: go-to-market results section
  → green Execution: team and hiring section

Wave 2: Review (depends on Wave 1)
  → cyan Planning: consistency check across sections
  → red Risk: risk section and decision items

Wave 3: Final (depends on Wave 2)
  → yellow Strategy: executive summary and narrative
  → green Execution: final deck assembly
```

---

## Cross-OS Safety Rules

1. **Read-only across OS boundaries** — FOUNDER:OS reads from other frameworks, never writes
2. **Never trigger operations in another OS** without explicit confirmation
3. **Financial data** — always verify against source before including in reports
4. **People data** — never include compensation or performance details without authorization
5. **Strategic documents** — mark as confidential, limit distribution
6. **Board materials** — require founder approval before distribution
7. **Delegation** — when action is needed, delegate to the appropriate OS framework with clear instructions
