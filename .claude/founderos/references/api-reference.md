# API Reference — FOUNDER:OS Cross-OS Safety Guide

FOUNDER:OS orchestrates across other OS frameworks (GTM:OS, FINANCE:OS, HR:OS, PRODUCT:OS, etc.). This document covers dangerous operations when coordinating across systems.

---

## Dangerous Cross-OS Operations

**HARD GATE — even in AUTO mode, always stop and confirm before any cross-system operation.**

**Rules:**
1. Never trigger operations in another OS framework without explicit confirmation
2. Cross-system writes have compounding blast radius — a mistake propagates
3. Always verify the target workspace/context before executing
4. Financial operations (FINANCE:OS, ad spend via ADS:OS) are always hard-gated
5. People operations (HR:OS terminations, role changes) require double confirmation
6. When in doubt, read-only. Never write across OS boundaries without asking.

---

### Cross-OS Danger Matrix

| Source | Target | Risk | Example |
|--------|--------|------|---------|
| FOUNDER:OS | FINANCE:OS | **CRITICAL** — real money | "Approve this invoice" triggers payment |
| FOUNDER:OS | HR:OS | **HIGH** — affects employment | "Offboard this person" triggers termination workflows |
| FOUNDER:OS | GTM:OS | **MEDIUM** — affects campaigns | "Ship this campaign" sends emails to real people |
| FOUNDER:OS | ADS:OS | **HIGH** — real ad spend | "Launch this campaign" starts spending money |
| FOUNDER:OS | LEGAL:OS | **MEDIUM** — affects agreements | "Send this contract" triggers signing workflow |
| FOUNDER:OS | CS:OS | **LOW** — affects support | "Close these tickets" ends customer conversations |
| FOUNDER:OS | PRODUCT:OS | **LOW** — affects roadmap | "Archive this project" removes work items |

### Hard Gates (never auto-approve)

These operations should ALWAYS stop for confirmation, regardless of execution mode:

1. **Any operation that moves money** — refunds, payments, ad spend, payroll
2. **Any operation that affects employment** — termination, offer changes, compensation changes
3. **Any operation that sends external communications** — emails, contracts, campaign launches
4. **Any operation that deletes data** — across any OS framework
5. **Any operation that changes permissions/access** — tool access, system access, document sharing

### Safe Operations (can auto-approve)

1. **Reading data** from any OS framework
2. **Generating reports** and dashboards
3. **Creating drafts** (not sending/publishing)
4. **Internal notes and annotations**
5. **Status checks and health monitoring**

---

### Slack API (api.slack.com)

**Auth:** Bot token `xoxb-...`
**Base URL:** `https://slack.com/api`

Used for executive notifications and cross-team coordination.

| Endpoint | Blast Radius | Irreversible? | Safe Alternative |
|----------|-------------|---------------|-----------------|
| `chat.postMessage` | Sends a message to a channel. All channel members see it. Cannot unsend. | YES — message visible | Draft messages for review before sending. |
| `chat.delete` | Deletes a message. Thread replies remain orphaned. | YES | Edit the message to correct instead. |
| `conversations.archive` | Archives a channel. All members lose posting ability. | NO — can unarchive | Generally safe for completed projects. |

**Rate limits:** Tier 1 (chat.postMessage): 1 per second. Tier 2: 20 per minute. Tier 3: 50 per minute.

---

### Exa API (api.exa.ai)

**Auth:** API key in header `x-api-key`
**Base URL:** `https://api.exa.ai`

Used for market research, competitive intelligence, and strategic research.

| Concern | Detail |
|---------|--------|
| **Credit model** | Per-search credits. Each search consumes credits regardless of result quality. |
| **No destructive endpoints** | Read-only API. No data deletion risk. |
| **Rate limits** | Varies by plan. Exceeding returns 429. |
| **Content caching** | Cache results locally to avoid duplicate searches. |

---

### Firecrawl API (api.firecrawl.dev)

**Auth:** Bearer token
**Base URL:** `https://api.firecrawl.dev/v1`

Used for web scraping and data extraction.

| Concern | Detail |
|---------|--------|
| **Credit model** | Per-page credits. Crawl operations can consume many credits (1 per page). |
| **Crawl blast radius** | `POST /crawl` with no `maxDepth` or `limit` can crawl an entire site. Always set `limit` and `maxDepth`. |
| **No destructive endpoints** | Read-only API. No external data deletion risk. |
| **Rate limits** | Varies by plan. Large crawls can burn through credits rapidly. |
| **Legal risk** | Scraping may violate target site ToS. Verify legal basis before crawling. |

---

## Danger Summary

| Category | Highest-Risk Operation | Worst Case |
|----------|----------------------|-----------|
| **Financial** | Triggering FINANCE:OS payment | Unauthorized payment processed |
| **Employment** | Triggering HR:OS termination | Employee wrongfully terminated |
| **Outbound** | Triggering GTM:OS campaign ship | Spam sent to real contacts |
| **Ad spend** | Triggering ADS:OS campaign launch | Budget burned on wrong audience |
| **Legal** | Triggering LEGAL:OS contract send | Wrong contract sent for signature |
| **Credit burn** | Unbounded Firecrawl crawl | Hundreds of credits consumed |

---

## Notes

- FOUNDER:OS is primarily a read + coordinate layer — it should rarely write directly to external systems
- Always delegate writes to the appropriate OS framework, which has its own safety gates
- Cross-OS dashboards and reports are safe — they only read
- When making strategic decisions, verify data freshness (check last sync timestamps)
- The reversible/irreversible decision framework applies to ALL cross-OS operations
