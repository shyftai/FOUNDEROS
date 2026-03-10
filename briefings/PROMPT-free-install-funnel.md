# Claude Code Prompt: Free Install Funnel

Paste this prompt into Claude Code when working in the Shyft AI website repo.

---

## The Prompt

```
Build the Antigravity OS free install tracking funnel. This captures opt-in registrations from 8 open-source OS frameworks (GTM:OS, CS:OS, CONTENT:OS, FINANCE:OS, HR:OS, INVESTOR:OS, COMMUNITY:OS, FOUNDER:OS) when users run their /onboard command.

## What already exists

Each OS framework's /onboard command already POSTs to `https://shyft.ai/api/hooks/register` with this payload:

{
  "os": "gtmos|csos|contentos|financeos|hros|investoros|communityos|founderos",
  "version": "1.4.0",
  "company": "Company Name",
  "email": "user@company.com",
  "workspace": "workspace-name",
  "timestamp": "ISO 8601"
}

Registration is opt-in, non-blocking, and fails silently.

## What to build

### 1. Supabase schema (run in SQL Editor or as migration)

Create these tables:

**installations** — every registration event
- id (UUID PK), os (TEXT, constrained to 8 valid values), version (TEXT, semver format), company (TEXT), email (TEXT, validated), workspace (TEXT), ip_address (INET), user_agent (TEXT), country_code (TEXT nullable), created_at (TIMESTAMPTZ)
- Indexes on: os, created_at DESC, email, company, (os + created_at)

**companies** — deduplicated from installations
- id (UUID PK), name (TEXT), normalized_name (TEXT UNIQUE, lowercase trimmed), email_domain (TEXT), first_seen (TIMESTAMPTZ), last_seen (TIMESTAMPTZ), install_count (INTEGER), os_frameworks (TEXT[]), emails (TEXT[]), created_at, updated_at
- Indexes on: normalized_name, email_domain, last_seen, install_count, os_frameworks (GIN)

**waitlist** — team tier interest (for when users hit the "team" button during onboard)
- id (UUID PK), email (TEXT), company (TEXT), os (TEXT), tier_interest (TEXT: team|business|enterprise), status (TEXT: pending|contacted|converted|declined), notes (TEXT), created_at, updated_at

**rate_limits** — per-IP rate limiting
- ip_address (INET PK), request_count (INTEGER), window_start (TIMESTAMPTZ), updated_at

Create these views:
- installs_by_os — COUNT grouped by os
- installs_by_week — weekly buckets for line charts
- company_os_matrix — which companies use which frameworks
- installs_daily — daily summary
- version_distribution — version breakdown per OS
- waitlist_summary — waitlist by tier, os, status

Enable RLS on all tables:
- service_role: full access (for edge functions)
- anon: SELECT only (for dashboard reads)

Create these database functions:
- check_rate_limit(ip, max_requests=10, window_minutes=60) → BOOLEAN
- upsert_company(company, email, os) → UUID — inserts or updates company record, deduplicates os_frameworks and emails arrays
- cleanup_rate_limits() → void — deletes expired windows
- get_dashboard_stats() → JSON — total installs, this week, this month, unique companies, unique users, waitlist count, frameworks active
- get_installs_by_os() → JSON — for pie chart
- get_install_trend(months=6) → JSON — weekly buckets for line chart

### 2. Supabase Edge Function: /register

File: supabase/functions/register/index.ts

TypeScript Deno edge function that:
- Accepts POST only, returns 405 for other methods
- Handles CORS preflight (OPTIONS)
- Validates required fields: os, version, company, email, timestamp
- Validates os is one of: gtmos, csos, contentos, financeos, hros, investoros, communityos, founderos
- Validates email format with regex
- Validates version is semver (X.Y.Z)
- Sanitizes all inputs (trim, strip HTML, cap at 500 chars)
- Checks rate limit via check_rate_limit RPC (10 req/IP/hour), returns 429 if exceeded
- Inserts into installations table
- Calls upsert_company RPC
- Sends Slack notification via SLACK_WEBHOOK_URL env var (if set):
  "New install: GTM:OS v1.4.0 by Acme Corp (jane@acme.com)"
- Returns {"status": "registered"} on success
- All errors return JSON with appropriate status codes (400, 429, 500)
- Uses SUPABASE_URL and SUPABASE_SERVICE_ROLE_KEY (auto-available in edge functions)

### 3. Supabase Edge Function: /waitlist

File: supabase/functions/waitlist/index.ts

Same pattern as /register but:
- Validates: email, company, os, tier_interest (team|business|enterprise)
- Inserts into waitlist table
- Slack notification: "Waitlist: Acme Corp interested in Enterprise tier for CS:OS"
- Rate limit: 5 req/IP/hour
- Returns {"status": "waitlisted"}

### 4. Dashboard page on the website

Create an admin dashboard page at /dashboard (or /admin/installs) that shows:

**Stats cards row:**
- Total installs (all time)
- This week
- This month
- Unique companies
- Unique users
- Waitlist signups
- Frameworks active (out of 8)

**Charts (use recharts or any chart lib already in the project):**
- Installs by OS framework (horizontal bar chart with OS colors)
- Install trend over time (line chart, weekly buckets, 6 months)

**Companies table:**
- Columns: Company, Domain, Installs, Frameworks (as badges), First Seen, Last Seen
- Sorted by install count descending
- Top 50

Use Supabase JS client with anon key + RLS for reads.
Cache API responses for 5 minutes (revalidate = 300).

OS color mapping for charts:
- gtmos: #FF8C00 (orange)
- csos: #4A90D9 (blue)
- contentos: #2ECC71 (teal)
- financeos: #27AE60 (green)
- hros: #E74C3C (coral)
- investoros: #9B59B6 (violet)
- communityos: #1ABC9C (cyan)
- founderos: #F1C40F (gold)

OS display names:
- gtmos → GTM:OS
- csos → CS:OS
- contentos → CONTENT:OS
- financeos → FINANCE:OS
- hros → HR:OS
- investoros → INVESTOR:OS
- communityos → COMMUNITY:OS
- founderos → FOUNDER:OS

### 5. DNS routing

The onboard commands POST to shyft.ai/api/hooks/register. Set up routing:

Option A (recommended): Cloudflare Worker that proxies /register and /waitlist to the Supabase edge function URLs
Option B: Vercel rewrite in vercel.json if the site is on Vercel
Option C: Direct Supabase function URL (for dev/testing)

Tell me which hosting setup the site uses and I'll configure the right option.

### 6. Environment variables needed

For Supabase edge functions (set via `supabase secrets set`):
- SLACK_WEBHOOK_URL — Slack incoming webhook for #antigravity-installs channel

For the website (.env.local):
- NEXT_PUBLIC_SUPABASE_URL — Supabase project URL
- NEXT_PUBLIC_SUPABASE_ANON_KEY — Supabase anon key (safe to expose, RLS restricts to reads)

## Implementation order

1. Create Supabase schema (tables, views, RLS, functions)
2. Deploy /register edge function
3. Deploy /waitlist edge function
4. Set up DNS routing
5. Build dashboard page
6. Test end-to-end with curl commands
7. Verify Slack notifications fire

## Testing

After building, test with:

curl -X POST https://shyft.ai/api/hooks/register \
  -H "Content-Type: application/json" \
  -d '{
    "os": "gtmos",
    "version": "1.4.0",
    "company": "Test Corp",
    "email": "test@testcorp.com",
    "workspace": "test",
    "timestamp": "2026-03-09T12:00:00Z"
  }'

Expected: {"status":"registered"}
```

---

## Context for the user

This prompt assumes:
- You have a Supabase project ready
- You have the Supabase CLI installed
- Your website is Next.js (adjust if different)
- You have a Slack workspace with incoming webhooks enabled

The full technical briefing with complete code for every component is at:
`FOUNDEROS/briefings/registration-endpoint.md`
