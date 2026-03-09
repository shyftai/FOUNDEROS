# Technical Briefing: Antigravity OS Registration and Telemetry System

**Status:** Ready for implementation
**Author:** Shyft AI engineering
**Date:** 2026-03-09
**Scope:** Supabase backend, edge functions, DNS routing, dashboard integration, Slack notifications

---

## Architecture Overview

```
+---------------------+       HTTPS POST        +-------------------------+
|  Claude Code CLI    | -----------------------> | hooks.shyftai.com       |
|  (8 OS frameworks)  |   /register              |   Cloudflare DNS/Proxy  |
|                     |   /waitlist               +----------+--------------+
+---------------------+                                     |
                                                             | proxy / rewrite
                                                             v
                                              +-----------------------------+
                                              | Supabase Edge Function      |
                                              |   - validate payload        |
                                              |   - sanitize inputs         |
                                              |   - insert installations    |
                                              |   - upsert companies        |
                                              |   - POST Slack webhook      |
                                              +----------+------------------+
                                                         |
                                                         v
                                              +-----------------------------+
                                              | Supabase PostgreSQL         |
                                              |   - installations           |
                                              |   - companies               |
                                              |   - usage_events            |
                                              |   - waitlist                |
                                              |   - views (analytics)       |
                                              +----------+------------------+
                                                         |
                                                         | anon key + RLS
                                                         v
                                              +-----------------------------+
                                              | shyftai.com/dashboard       |
                                              |   Next.js frontend          |
                                              |   - install metrics         |
                                              |   - company list            |
                                              |   - waitlist pipeline       |
                                              +-----------------------------+
```

### Data Flow

1. User runs `/[prefix]:onboard` in any OS framework
2. Onboarding asks "Register for updates?" -- opt-in only
3. If yes, Claude Code sends `POST https://hooks.shyftai.com/register`
4. Cloudflare proxies to Supabase edge function
5. Edge function validates, inserts, upserts, notifies Slack
6. Dashboard reads data via Supabase client with anon key + RLS

### OS Framework Registry

| OS           | Prefix       | Repo Directory  |
|------------- |------------- |-----------------|
| GTM:OS       | `gtmos`      | GTMOS           |
| CS:OS        | `csos`       | CSOS            |
| CONTENT:OS   | `contentos`  | CONTENTOS       |
| FINANCE:OS   | `financeos`  | FINANCEOS       |
| HR:OS        | `hros`       | HROS            |
| INVESTOR:OS  | `investoros` | INVESTOROS      |
| COMMUNITY:OS | `communityos`| COMMUNITYOS     |
| FOUNDER:OS   | `founderos`  | FOUNDEROS       |

---

## Prerequisites

Before starting implementation, ensure you have:

- [ ] A Supabase project created (free tier is fine to start)
- [ ] Supabase project URL (`https://<project-ref>.supabase.co`)
- [ ] Supabase anon key (for dashboard reads)
- [ ] Supabase service role key (for edge function writes)
- [ ] Supabase CLI installed (`npm i -g supabase`)
- [ ] Access to Cloudflare DNS for `shyftai.com`
- [ ] A Slack incoming webhook URL for notifications
- [ ] Node.js 18+ (for edge function development)

---

## Implementation Order

Execute in this order -- each step depends on the previous:

1. **Database schema** -- tables, indexes, RLS policies, views
2. **Edge function: /register** -- validate, insert, upsert, notify
3. **Edge function: /waitlist** -- validate, insert, notify
4. **DNS routing** -- point hooks.shyftai.com to Supabase
5. **Dashboard queries** -- SQL for all metrics
6. **Website integration** -- Supabase client, API routes, components
7. **Testing** -- end-to-end verification
8. **Monitoring** -- alerts, error tracking

---

## Step 1: Database Schema

Run these statements in Supabase SQL Editor or as a migration file.

### Migration file: `supabase/migrations/001_registration_schema.sql`

```sql
-- ============================================================
-- Antigravity OS Registration System
-- Migration: 001_registration_schema.sql
-- ============================================================

-- Enable required extensions
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
CREATE EXTENSION IF NOT EXISTS "pg_trgm";  -- for text search on company names


-- ------------------------------------------------------------
-- TABLE: installations
-- Every registration event from onboarding
-- ------------------------------------------------------------
CREATE TABLE installations (
    id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    os              TEXT NOT NULL,
    version         TEXT NOT NULL,
    company         TEXT NOT NULL,
    email           TEXT NOT NULL,
    workspace       TEXT NOT NULL,
    ip_address      INET,
    user_agent      TEXT,
    country_code    TEXT,           -- derived from IP if geolocation added
    region          TEXT,           -- derived from IP if geolocation added
    created_at      TIMESTAMPTZ NOT NULL DEFAULT NOW(),

    -- Constraints
    CONSTRAINT valid_os CHECK (os IN (
        'gtmos', 'csos', 'contentos', 'financeos',
        'hros', 'investoros', 'communityos', 'founderos'
    )),
    CONSTRAINT valid_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'),
    CONSTRAINT valid_version CHECK (version ~* '^\d+\.\d+\.\d+$')
);

-- Indexes for common query patterns
CREATE INDEX idx_installations_os ON installations (os);
CREATE INDEX idx_installations_created_at ON installations (created_at DESC);
CREATE INDEX idx_installations_email ON installations (email);
CREATE INDEX idx_installations_company ON installations (company);
CREATE INDEX idx_installations_os_created ON installations (os, created_at DESC);


-- ------------------------------------------------------------
-- TABLE: companies
-- Deduplicated company records derived from installations
-- ------------------------------------------------------------
CREATE TABLE companies (
    id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    name            TEXT NOT NULL,
    normalized_name TEXT NOT NULL UNIQUE,  -- lowercase, trimmed for dedup
    email_domain    TEXT NOT NULL,         -- extracted from first email
    first_seen      TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    last_seen       TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    install_count   INTEGER NOT NULL DEFAULT 1,
    os_frameworks   TEXT[] NOT NULL DEFAULT '{}',  -- array of os names used
    emails          TEXT[] NOT NULL DEFAULT '{}',   -- all emails seen
    created_at      TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at      TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_companies_normalized_name ON companies (normalized_name);
CREATE INDEX idx_companies_email_domain ON companies (email_domain);
CREATE INDEX idx_companies_last_seen ON companies (last_seen DESC);
CREATE INDEX idx_companies_install_count ON companies (install_count DESC);
CREATE INDEX idx_companies_os_frameworks ON companies USING GIN (os_frameworks);


-- ------------------------------------------------------------
-- TABLE: usage_events
-- Future expansion: track active usage (heartbeats, commands)
-- ------------------------------------------------------------
CREATE TABLE usage_events (
    id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    installation_id UUID REFERENCES installations(id),
    os              TEXT NOT NULL,
    event_type      TEXT NOT NULL,       -- 'heartbeat', 'command', 'error', 'upgrade'
    event_name      TEXT,                -- e.g. 'gtm:onboard', 'cs:health-check'
    metadata        JSONB DEFAULT '{}',  -- flexible payload for any event data
    version         TEXT,
    workspace       TEXT,
    created_at      TIMESTAMPTZ NOT NULL DEFAULT NOW(),

    CONSTRAINT valid_usage_os CHECK (os IN (
        'gtmos', 'csos', 'contentos', 'financeos',
        'hros', 'investoros', 'communityos', 'founderos'
    )),
    CONSTRAINT valid_event_type CHECK (event_type IN (
        'heartbeat', 'command', 'error', 'upgrade', 'feature_use'
    ))
);

CREATE INDEX idx_usage_events_os ON usage_events (os);
CREATE INDEX idx_usage_events_type ON usage_events (event_type);
CREATE INDEX idx_usage_events_created ON usage_events (created_at DESC);
CREATE INDEX idx_usage_events_installation ON usage_events (installation_id);


-- ------------------------------------------------------------
-- TABLE: waitlist
-- Team/collab tier interest signups
-- ------------------------------------------------------------
CREATE TABLE waitlist (
    id              UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    email           TEXT NOT NULL,
    company         TEXT NOT NULL,
    os              TEXT NOT NULL,
    tier_interest   TEXT NOT NULL,
    notes           TEXT,
    status          TEXT NOT NULL DEFAULT 'pending',  -- pending, contacted, converted, declined
    created_at      TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at      TIMESTAMPTZ NOT NULL DEFAULT NOW(),

    CONSTRAINT valid_waitlist_os CHECK (os IN (
        'gtmos', 'csos', 'contentos', 'financeos',
        'hros', 'investoros', 'communityos', 'founderos'
    )),
    CONSTRAINT valid_tier CHECK (tier_interest IN ('team', 'business', 'enterprise')),
    CONSTRAINT valid_status CHECK (status IN ('pending', 'contacted', 'converted', 'declined')),
    CONSTRAINT valid_waitlist_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$')
);

CREATE INDEX idx_waitlist_email ON waitlist (email);
CREATE INDEX idx_waitlist_tier ON waitlist (tier_interest);
CREATE INDEX idx_waitlist_status ON waitlist (status);
CREATE INDEX idx_waitlist_created ON waitlist (created_at DESC);


-- ------------------------------------------------------------
-- TABLE: rate_limits
-- Track request rates per IP for edge function rate limiting
-- ------------------------------------------------------------
CREATE TABLE rate_limits (
    ip_address      INET PRIMARY KEY,
    request_count   INTEGER NOT NULL DEFAULT 1,
    window_start    TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at      TIMESTAMPTZ NOT NULL DEFAULT NOW()
);


-- ============================================================
-- VIEWS
-- ============================================================

-- Installs by OS framework
CREATE OR REPLACE VIEW installs_by_os AS
SELECT
    os,
    COUNT(*) AS total_installs,
    COUNT(DISTINCT email) AS unique_users,
    COUNT(DISTINCT company) AS unique_companies,
    MIN(created_at) AS first_install,
    MAX(created_at) AS last_install
FROM installations
GROUP BY os
ORDER BY total_installs DESC;


-- Installs by week (for line charts)
CREATE OR REPLACE VIEW installs_by_week AS
SELECT
    DATE_TRUNC('week', created_at)::DATE AS week_start,
    os,
    COUNT(*) AS installs
FROM installations
GROUP BY DATE_TRUNC('week', created_at), os
ORDER BY week_start DESC, os;


-- Company-OS matrix: which companies use which frameworks
CREATE OR REPLACE VIEW company_os_matrix AS
SELECT
    c.name AS company,
    c.email_domain,
    c.install_count,
    c.os_frameworks,
    ARRAY_LENGTH(c.os_frameworks, 1) AS frameworks_used,
    c.first_seen,
    c.last_seen
FROM companies c
ORDER BY c.install_count DESC;


-- Daily install summary (for dashboards)
CREATE OR REPLACE VIEW installs_daily AS
SELECT
    DATE_TRUNC('day', created_at)::DATE AS day,
    COUNT(*) AS installs,
    COUNT(DISTINCT company) AS unique_companies,
    COUNT(DISTINCT email) AS unique_users
FROM installations
GROUP BY DATE_TRUNC('day', created_at)
ORDER BY day DESC;


-- Version distribution per OS
CREATE OR REPLACE VIEW version_distribution AS
SELECT
    os,
    version,
    COUNT(*) AS install_count,
    ROUND(
        COUNT(*)::NUMERIC / SUM(COUNT(*)) OVER (PARTITION BY os) * 100,
        1
    ) AS percentage
FROM installations
GROUP BY os, version
ORDER BY os, install_count DESC;


-- Waitlist summary
CREATE OR REPLACE VIEW waitlist_summary AS
SELECT
    tier_interest,
    os,
    status,
    COUNT(*) AS signups,
    MIN(created_at) AS first_signup,
    MAX(created_at) AS last_signup
FROM waitlist
GROUP BY tier_interest, os, status
ORDER BY signups DESC;


-- ============================================================
-- ROW LEVEL SECURITY
-- ============================================================

-- Enable RLS on all tables
ALTER TABLE installations ENABLE ROW LEVEL SECURITY;
ALTER TABLE companies ENABLE ROW LEVEL SECURITY;
ALTER TABLE usage_events ENABLE ROW LEVEL SECURITY;
ALTER TABLE waitlist ENABLE ROW LEVEL SECURITY;
ALTER TABLE rate_limits ENABLE ROW LEVEL SECURITY;

-- Policy: Edge functions (service role) can insert into installations
CREATE POLICY "service_insert_installations"
    ON installations FOR INSERT
    TO service_role
    WITH CHECK (true);

-- Policy: Edge functions (service role) can read installations
CREATE POLICY "service_read_installations"
    ON installations FOR SELECT
    TO service_role
    USING (true);

-- Policy: Anon users can read installations (for dashboard)
-- Restrict to aggregated views in production if needed
CREATE POLICY "anon_read_installations"
    ON installations FOR SELECT
    TO anon
    USING (true);

-- Policy: Service role full access to companies
CREATE POLICY "service_all_companies"
    ON companies FOR ALL
    TO service_role
    USING (true)
    WITH CHECK (true);

-- Policy: Anon can read companies (for dashboard)
CREATE POLICY "anon_read_companies"
    ON companies FOR SELECT
    TO anon
    USING (true);

-- Policy: Service role full access to usage_events
CREATE POLICY "service_all_usage_events"
    ON usage_events FOR ALL
    TO service_role
    USING (true)
    WITH CHECK (true);

-- Policy: Anon can read usage_events (for dashboard)
CREATE POLICY "anon_read_usage_events"
    ON usage_events FOR SELECT
    TO anon
    USING (true);

-- Policy: Service role full access to waitlist
CREATE POLICY "service_all_waitlist"
    ON waitlist FOR ALL
    TO service_role
    USING (true)
    WITH CHECK (true);

-- Policy: Anon can read waitlist (for dashboard)
CREATE POLICY "anon_read_waitlist"
    ON waitlist FOR SELECT
    TO anon
    USING (true);

-- Policy: Service role full access to rate_limits
CREATE POLICY "service_all_rate_limits"
    ON rate_limits FOR ALL
    TO service_role
    USING (true)
    WITH CHECK (true);


-- ============================================================
-- FUNCTIONS
-- ============================================================

-- Function to clean up expired rate limit windows (run via pg_cron or manually)
CREATE OR REPLACE FUNCTION cleanup_rate_limits()
RETURNS void AS $$
BEGIN
    DELETE FROM rate_limits
    WHERE window_start < NOW() - INTERVAL '1 hour';
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Function to check and update rate limit
-- Returns true if request is allowed, false if rate limited
CREATE OR REPLACE FUNCTION check_rate_limit(
    p_ip INET,
    p_max_requests INTEGER DEFAULT 10,
    p_window_minutes INTEGER DEFAULT 60
)
RETURNS BOOLEAN AS $$
DECLARE
    v_count INTEGER;
    v_window_start TIMESTAMPTZ;
BEGIN
    SELECT request_count, window_start
    INTO v_count, v_window_start
    FROM rate_limits
    WHERE ip_address = p_ip;

    IF NOT FOUND THEN
        -- First request from this IP
        INSERT INTO rate_limits (ip_address, request_count, window_start)
        VALUES (p_ip, 1, NOW());
        RETURN true;
    END IF;

    IF v_window_start < NOW() - (p_window_minutes || ' minutes')::INTERVAL THEN
        -- Window expired, reset
        UPDATE rate_limits
        SET request_count = 1, window_start = NOW(), updated_at = NOW()
        WHERE ip_address = p_ip;
        RETURN true;
    END IF;

    IF v_count >= p_max_requests THEN
        -- Rate limited
        RETURN false;
    END IF;

    -- Increment counter
    UPDATE rate_limits
    SET request_count = request_count + 1, updated_at = NOW()
    WHERE ip_address = p_ip;
    RETURN true;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Function to upsert company record
CREATE OR REPLACE FUNCTION upsert_company(
    p_company TEXT,
    p_email TEXT,
    p_os TEXT
)
RETURNS UUID AS $$
DECLARE
    v_normalized TEXT;
    v_domain TEXT;
    v_company_id UUID;
BEGIN
    v_normalized := LOWER(TRIM(p_company));
    v_domain := SPLIT_PART(p_email, '@', 2);

    INSERT INTO companies (name, normalized_name, email_domain, os_frameworks, emails)
    VALUES (
        TRIM(p_company),
        v_normalized,
        v_domain,
        ARRAY[p_os],
        ARRAY[LOWER(TRIM(p_email))]
    )
    ON CONFLICT (normalized_name) DO UPDATE SET
        last_seen = NOW(),
        install_count = companies.install_count + 1,
        os_frameworks = (
            SELECT ARRAY(SELECT DISTINCT UNNEST(companies.os_frameworks || ARRAY[p_os]))
        ),
        emails = (
            SELECT ARRAY(SELECT DISTINCT UNNEST(companies.emails || ARRAY[LOWER(TRIM(p_email))]))
        ),
        updated_at = NOW()
    RETURNING id INTO v_company_id;

    RETURN v_company_id;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;
```

---

## Step 2: Edge Function -- /register

### File: `supabase/functions/register/index.ts`

```typescript
import { serve } from "https://deno.land/std@0.177.0/http/server.ts";
import { createClient } from "https://esm.sh/@supabase/supabase-js@2.39.0";

const VALID_OS = [
  "gtmos",
  "csos",
  "contentos",
  "financeos",
  "hros",
  "investoros",
  "communityos",
  "founderos",
] as const;

type ValidOS = (typeof VALID_OS)[number];

interface RegistrationPayload {
  os: string;
  version: string;
  company: string;
  email: string;
  workspace: string;
  timestamp: string;
}

const corsHeaders = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Headers":
    "authorization, x-client-info, apikey, content-type",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
};

function sanitize(input: string): string {
  return input
    .trim()
    .replace(/[<>]/g, "") // strip HTML angle brackets
    .slice(0, 500); // cap length
}

function isValidEmail(email: string): boolean {
  return /^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$/.test(email);
}

function isValidVersion(version: string): boolean {
  return /^\d+\.\d+\.\d+$/.test(version);
}

function isValidOS(os: string): os is ValidOS {
  return VALID_OS.includes(os as ValidOS);
}

async function sendSlackNotification(
  webhookUrl: string,
  message: string
): Promise<void> {
  try {
    await fetch(webhookUrl, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ text: message }),
    });
  } catch {
    // Slack notification is non-critical -- fail silently
    console.error("Failed to send Slack notification");
  }
}

serve(async (req: Request) => {
  // Handle CORS preflight
  if (req.method === "OPTIONS") {
    return new Response("ok", { headers: corsHeaders });
  }

  if (req.method !== "POST") {
    return new Response(
      JSON.stringify({ error: "Method not allowed" }),
      {
        status: 405,
        headers: { ...corsHeaders, "Content-Type": "application/json" },
      }
    );
  }

  try {
    // Parse body
    let body: RegistrationPayload;
    try {
      body = await req.json();
    } catch {
      return new Response(
        JSON.stringify({ error: "Invalid JSON body" }),
        {
          status: 400,
          headers: { ...corsHeaders, "Content-Type": "application/json" },
        }
      );
    }

    // Validate required fields
    const requiredFields: (keyof RegistrationPayload)[] = [
      "os",
      "version",
      "company",
      "email",
      "timestamp",
    ];
    const missingFields = requiredFields.filter(
      (f) => !body[f] || typeof body[f] !== "string" || body[f].trim() === ""
    );

    if (missingFields.length > 0) {
      return new Response(
        JSON.stringify({
          error: "Missing required fields",
          fields: missingFields,
        }),
        {
          status: 400,
          headers: { ...corsHeaders, "Content-Type": "application/json" },
        }
      );
    }

    // Sanitize inputs
    const os = sanitize(body.os).toLowerCase();
    const version = sanitize(body.version);
    const company = sanitize(body.company);
    const email = sanitize(body.email).toLowerCase();
    const workspace = sanitize(body.workspace || "default");
    const timestamp = sanitize(body.timestamp);

    // Validate OS
    if (!isValidOS(os)) {
      return new Response(
        JSON.stringify({
          error: "Invalid OS framework",
          valid_values: VALID_OS,
        }),
        {
          status: 400,
          headers: { ...corsHeaders, "Content-Type": "application/json" },
        }
      );
    }

    // Validate email format
    if (!isValidEmail(email)) {
      return new Response(
        JSON.stringify({ error: "Invalid email format" }),
        {
          status: 400,
          headers: { ...corsHeaders, "Content-Type": "application/json" },
        }
      );
    }

    // Validate version format
    if (!isValidVersion(version)) {
      return new Response(
        JSON.stringify({
          error: "Invalid version format. Expected: X.Y.Z",
        }),
        {
          status: 400,
          headers: { ...corsHeaders, "Content-Type": "application/json" },
        }
      );
    }

    // Initialize Supabase client with service role key
    const supabaseUrl = Deno.env.get("SUPABASE_URL")!;
    const supabaseServiceKey = Deno.env.get("SUPABASE_SERVICE_ROLE_KEY")!;
    const supabase = createClient(supabaseUrl, supabaseServiceKey);

    // Check rate limit (10 requests per IP per hour)
    const clientIp =
      req.headers.get("x-forwarded-for")?.split(",")[0]?.trim() ||
      req.headers.get("cf-connecting-ip") ||
      "0.0.0.0";

    const { data: rateLimitOk } = await supabase.rpc("check_rate_limit", {
      p_ip: clientIp,
      p_max_requests: 10,
      p_window_minutes: 60,
    });

    if (rateLimitOk === false) {
      return new Response(
        JSON.stringify({ error: "Rate limit exceeded. Try again later." }),
        {
          status: 429,
          headers: {
            ...corsHeaders,
            "Content-Type": "application/json",
            "Retry-After": "3600",
          },
        }
      );
    }

    // Insert into installations
    const { error: insertError } = await supabase
      .from("installations")
      .insert({
        os,
        version,
        company,
        email,
        workspace,
        ip_address: clientIp,
        user_agent: req.headers.get("user-agent") || null,
        created_at: timestamp,
      });

    if (insertError) {
      console.error("Insert error:", insertError);
      return new Response(
        JSON.stringify({ error: "Registration failed" }),
        {
          status: 500,
          headers: { ...corsHeaders, "Content-Type": "application/json" },
        }
      );
    }

    // Upsert company record
    const { error: upsertError } = await supabase.rpc("upsert_company", {
      p_company: company,
      p_email: email,
      p_os: os,
    });

    if (upsertError) {
      // Non-critical -- log but don't fail the registration
      console.error("Company upsert error:", upsertError);
    }

    // Send Slack notification
    const slackWebhookUrl = Deno.env.get("SLACK_WEBHOOK_URL");
    if (slackWebhookUrl) {
      const osDisplay: Record<string, string> = {
        gtmos: "GTM:OS",
        csos: "CS:OS",
        contentos: "CONTENT:OS",
        financeos: "FINANCE:OS",
        hros: "HR:OS",
        investoros: "INVESTOR:OS",
        communityos: "COMMUNITY:OS",
        founderos: "FOUNDER:OS",
      };
      const message =
        `New install: ${osDisplay[os] || os} v${version} by ${company} (${email})`;
      await sendSlackNotification(slackWebhookUrl, message);
    }

    return new Response(
      JSON.stringify({ status: "registered" }),
      {
        status: 200,
        headers: { ...corsHeaders, "Content-Type": "application/json" },
      }
    );
  } catch (err) {
    console.error("Unexpected error:", err);
    return new Response(
      JSON.stringify({ error: "Internal server error" }),
      {
        status: 500,
        headers: { ...corsHeaders, "Content-Type": "application/json" },
      }
    );
  }
});
```

---

## Step 3: Edge Function -- /waitlist

### File: `supabase/functions/waitlist/index.ts`

```typescript
import { serve } from "https://deno.land/std@0.177.0/http/server.ts";
import { createClient } from "https://esm.sh/@supabase/supabase-js@2.39.0";

const VALID_OS = [
  "gtmos", "csos", "contentos", "financeos",
  "hros", "investoros", "communityos", "founderos",
] as const;

const VALID_TIERS = ["team", "business", "enterprise"] as const;

const corsHeaders = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Headers":
    "authorization, x-client-info, apikey, content-type",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
};

function sanitize(input: string): string {
  return input.trim().replace(/[<>]/g, "").slice(0, 500);
}

function isValidEmail(email: string): boolean {
  return /^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$/.test(email);
}

serve(async (req: Request) => {
  if (req.method === "OPTIONS") {
    return new Response("ok", { headers: corsHeaders });
  }

  if (req.method !== "POST") {
    return new Response(
      JSON.stringify({ error: "Method not allowed" }),
      { status: 405, headers: { ...corsHeaders, "Content-Type": "application/json" } }
    );
  }

  try {
    let body: { email: string; company: string; os: string; tier_interest: string };
    try {
      body = await req.json();
    } catch {
      return new Response(
        JSON.stringify({ error: "Invalid JSON body" }),
        { status: 400, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    // Validate required fields
    for (const field of ["email", "company", "os", "tier_interest"] as const) {
      if (!body[field] || typeof body[field] !== "string" || body[field].trim() === "") {
        return new Response(
          JSON.stringify({ error: `Missing required field: ${field}` }),
          { status: 400, headers: { ...corsHeaders, "Content-Type": "application/json" } }
        );
      }
    }

    const email = sanitize(body.email).toLowerCase();
    const company = sanitize(body.company);
    const os = sanitize(body.os).toLowerCase();
    const tierInterest = sanitize(body.tier_interest).toLowerCase();

    if (!isValidEmail(email)) {
      return new Response(
        JSON.stringify({ error: "Invalid email format" }),
        { status: 400, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    if (!VALID_OS.includes(os as any)) {
      return new Response(
        JSON.stringify({ error: "Invalid OS framework" }),
        { status: 400, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    if (!VALID_TIERS.includes(tierInterest as any)) {
      return new Response(
        JSON.stringify({ error: "Invalid tier. Must be: team, business, or enterprise" }),
        { status: 400, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    const supabaseUrl = Deno.env.get("SUPABASE_URL")!;
    const supabaseServiceKey = Deno.env.get("SUPABASE_SERVICE_ROLE_KEY")!;
    const supabase = createClient(supabaseUrl, supabaseServiceKey);

    // Rate limit check
    const clientIp =
      req.headers.get("x-forwarded-for")?.split(",")[0]?.trim() ||
      req.headers.get("cf-connecting-ip") ||
      "0.0.0.0";

    const { data: rateLimitOk } = await supabase.rpc("check_rate_limit", {
      p_ip: clientIp,
      p_max_requests: 5,
      p_window_minutes: 60,
    });

    if (rateLimitOk === false) {
      return new Response(
        JSON.stringify({ error: "Rate limit exceeded" }),
        { status: 429, headers: { ...corsHeaders, "Content-Type": "application/json", "Retry-After": "3600" } }
      );
    }

    // Insert into waitlist
    const { error: insertError } = await supabase.from("waitlist").insert({
      email,
      company,
      os,
      tier_interest: tierInterest,
    });

    if (insertError) {
      console.error("Waitlist insert error:", insertError);
      return new Response(
        JSON.stringify({ error: "Waitlist registration failed" }),
        { status: 500, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    // Slack notification
    const slackWebhookUrl = Deno.env.get("SLACK_WEBHOOK_URL");
    if (slackWebhookUrl) {
      const osDisplay: Record<string, string> = {
        gtmos: "GTM:OS", csos: "CS:OS", contentos: "CONTENT:OS",
        financeos: "FINANCE:OS", hros: "HR:OS", investoros: "INVESTOR:OS",
        communityos: "COMMUNITY:OS", founderos: "FOUNDER:OS",
      };
      const tierDisplay = tierInterest.charAt(0).toUpperCase() + tierInterest.slice(1);
      const message =
        `Waitlist: ${company} interested in ${tierDisplay} tier for ${osDisplay[os] || os}`;
      try {
        await fetch(slackWebhookUrl, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ text: message }),
        });
      } catch {
        console.error("Failed to send Slack notification");
      }
    }

    return new Response(
      JSON.stringify({ status: "waitlisted" }),
      { status: 200, headers: { ...corsHeaders, "Content-Type": "application/json" } }
    );
  } catch (err) {
    console.error("Unexpected error:", err);
    return new Response(
      JSON.stringify({ error: "Internal server error" }),
      { status: 500, headers: { ...corsHeaders, "Content-Type": "application/json" } }
    );
  }
});
```

---

## Step 4: DNS / Routing

Three options for routing `hooks.shyftai.com/register` to the Supabase edge function.

### Option A: Cloudflare Worker (recommended)

**Pros:** Full control, custom domain, path-based routing, analytics, WAF protection, free tier generous
**Cons:** Extra layer to maintain, Cloudflare account required

```
DNS: hooks.shyftai.com -> Cloudflare (proxied, orange cloud)
```

Cloudflare Worker code:

```javascript
// wrangler.toml
// name = "antigravity-hooks"
// main = "src/index.js"
// compatibility_date = "2024-01-01"
// [vars]
// SUPABASE_FUNCTION_BASE = "https://<project-ref>.supabase.co/functions/v1"

export default {
  async fetch(request, env) {
    const url = new URL(request.url);

    // Route based on path
    const routes = {
      "/register": `${env.SUPABASE_FUNCTION_BASE}/register`,
      "/waitlist": `${env.SUPABASE_FUNCTION_BASE}/waitlist`,
    };

    const target = routes[url.pathname];
    if (!target) {
      return new Response(JSON.stringify({ error: "Not found" }), {
        status: 404,
        headers: { "Content-Type": "application/json" },
      });
    }

    // Forward the request to Supabase
    const headers = new Headers(request.headers);
    headers.set("Authorization", `Bearer ${env.SUPABASE_ANON_KEY}`);

    const response = await fetch(target, {
      method: request.method,
      headers,
      body: request.method !== "GET" ? request.body : undefined,
    });

    // Forward response back with CORS headers
    const responseHeaders = new Headers(response.headers);
    responseHeaders.set("Access-Control-Allow-Origin", "*");

    return new Response(response.body, {
      status: response.status,
      headers: responseHeaders,
    });
  },
};
```

**Setup steps:**
1. `npm create cloudflare@latest antigravity-hooks` -- select Worker
2. Add the code above
3. `npx wrangler secret put SUPABASE_ANON_KEY` -- paste your anon key
4. Set `SUPABASE_FUNCTION_BASE` in wrangler.toml
5. `npx wrangler deploy`
6. In Cloudflare DNS, add CNAME record: `hooks` -> `antigravity-hooks.<account>.workers.dev` (proxied)
7. Or use `npx wrangler routes add hooks.shyftai.com/*`

### Option B: Vercel Rewrite

**Pros:** Simple if Shyft AI website is already on Vercel, no extra service
**Cons:** Tied to Vercel deployment, slight latency from rewrite

In `vercel.json` on the shyftai.com project:

```json
{
  "rewrites": [
    {
      "source": "/hooks/register",
      "destination": "https://<project-ref>.supabase.co/functions/v1/register"
    },
    {
      "source": "/hooks/waitlist",
      "destination": "https://<project-ref>.supabase.co/functions/v1/waitlist"
    }
  ]
}
```

Then DNS: `hooks.shyftai.com` CNAME to `cname.vercel-dns.com`

### Option C: Direct Supabase Function URL

**Pros:** Zero infrastructure, immediate, free
**Cons:** Exposes Supabase project URL, no custom domain, harder to migrate later

URL pattern: `https://<project-ref>.supabase.co/functions/v1/register`

Update all OS framework onboard commands to POST directly to this URL.

### Recommendation

**Use Option A (Cloudflare Worker)** for production:
- Custom domain with hooks.shyftai.com
- Path-based routing for multiple endpoints
- Built-in DDoS protection and analytics
- Easy to add new endpoints later
- Can add geographic data from `cf-ipcountry` header

**Use Option C (direct URL) for development/testing** -- no setup required.

---

## Step 5: Dashboard Queries

These queries can be used directly from the Supabase JS client or as database functions.

### 5.1 Total Installs

```sql
-- All time
SELECT COUNT(*) AS total FROM installations;

-- This week
SELECT COUNT(*) AS this_week
FROM installations
WHERE created_at >= DATE_TRUNC('week', NOW());

-- This month
SELECT COUNT(*) AS this_month
FROM installations
WHERE created_at >= DATE_TRUNC('month', NOW());

-- Combined summary
SELECT
    COUNT(*) AS all_time,
    COUNT(*) FILTER (WHERE created_at >= DATE_TRUNC('week', NOW())) AS this_week,
    COUNT(*) FILTER (WHERE created_at >= DATE_TRUNC('month', NOW())) AS this_month,
    COUNT(DISTINCT email) AS unique_users,
    COUNT(DISTINCT company) AS unique_companies
FROM installations;
```

### 5.2 Installs by OS (pie chart data)

```sql
SELECT
    os,
    COUNT(*) AS installs,
    ROUND(COUNT(*)::NUMERIC / SUM(COUNT(*)) OVER () * 100, 1) AS percentage
FROM installations
GROUP BY os
ORDER BY installs DESC;
```

### 5.3 Installs Over Time (line chart, weekly buckets)

```sql
SELECT
    DATE_TRUNC('week', created_at)::DATE AS week,
    os,
    COUNT(*) AS installs
FROM installations
WHERE created_at >= NOW() - INTERVAL '6 months'
GROUP BY week, os
ORDER BY week ASC, os;

-- Simplified (all OS combined)
SELECT
    DATE_TRUNC('week', created_at)::DATE AS week,
    COUNT(*) AS installs
FROM installations
WHERE created_at >= NOW() - INTERVAL '6 months'
GROUP BY week
ORDER BY week ASC;
```

### 5.4 Top Companies by Install Count

```sql
SELECT
    name AS company,
    email_domain,
    install_count,
    os_frameworks,
    ARRAY_LENGTH(os_frameworks, 1) AS frameworks_used,
    first_seen,
    last_seen
FROM companies
ORDER BY install_count DESC
LIMIT 20;
```

### 5.5 Version Distribution per OS

```sql
SELECT
    os,
    version,
    COUNT(*) AS installs,
    ROUND(COUNT(*)::NUMERIC / SUM(COUNT(*)) OVER (PARTITION BY os) * 100, 1) AS pct
FROM installations
GROUP BY os, version
ORDER BY os, installs DESC;
```

### 5.6 New Companies This Week

```sql
SELECT
    name,
    email_domain,
    os_frameworks,
    first_seen
FROM companies
WHERE first_seen >= DATE_TRUNC('week', NOW())
ORDER BY first_seen DESC;
```

### 5.7 Geographic Distribution (requires IP geolocation)

If using Cloudflare Worker (Option A), the `cf-ipcountry` header provides country code for free. Store it in `country_code` column.

```sql
SELECT
    country_code,
    COUNT(*) AS installs,
    COUNT(DISTINCT company) AS companies
FROM installations
WHERE country_code IS NOT NULL
GROUP BY country_code
ORDER BY installs DESC;
```

### 5.8 Conversion Funnel

```sql
SELECT
    'installations' AS stage,
    COUNT(DISTINCT email) AS users
FROM installations

UNION ALL

SELECT
    'waitlist' AS stage,
    COUNT(DISTINCT email) AS users
FROM waitlist

UNION ALL

SELECT
    'waitlist_by_tier' AS stage,
    COUNT(DISTINCT email) AS users
FROM waitlist
WHERE tier_interest = 'enterprise'  -- parameterize tier

ORDER BY
    CASE stage
        WHEN 'installations' THEN 1
        WHEN 'waitlist' THEN 2
        WHEN 'waitlist_by_tier' THEN 3
    END;
```

### 5.9 Create Database Functions for Dashboard

Wrap the most common queries as database functions so the frontend can call them via `supabase.rpc()`:

```sql
-- Summary stats for the dashboard header
CREATE OR REPLACE FUNCTION get_dashboard_stats()
RETURNS JSON AS $$
BEGIN
    RETURN (
        SELECT json_build_object(
            'total_installs', (SELECT COUNT(*) FROM installations),
            'this_week', (SELECT COUNT(*) FROM installations WHERE created_at >= DATE_TRUNC('week', NOW())),
            'this_month', (SELECT COUNT(*) FROM installations WHERE created_at >= DATE_TRUNC('month', NOW())),
            'unique_companies', (SELECT COUNT(*) FROM companies),
            'unique_users', (SELECT COUNT(DISTINCT email) FROM installations),
            'waitlist_count', (SELECT COUNT(*) FROM waitlist WHERE status = 'pending'),
            'frameworks_active', (SELECT COUNT(DISTINCT os) FROM installations)
        )
    );
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Installs by OS for pie chart
CREATE OR REPLACE FUNCTION get_installs_by_os()
RETURNS JSON AS $$
BEGIN
    RETURN (
        SELECT json_agg(row_to_json(t))
        FROM (
            SELECT os, COUNT(*) AS installs,
                ROUND(COUNT(*)::NUMERIC / NULLIF(SUM(COUNT(*)) OVER (), 0) * 100, 1) AS percentage
            FROM installations
            GROUP BY os
            ORDER BY installs DESC
        ) t
    );
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Weekly install trend for line chart
CREATE OR REPLACE FUNCTION get_install_trend(months INTEGER DEFAULT 6)
RETURNS JSON AS $$
BEGIN
    RETURN (
        SELECT json_agg(row_to_json(t))
        FROM (
            SELECT
                DATE_TRUNC('week', created_at)::DATE AS week,
                os,
                COUNT(*) AS installs
            FROM installations
            WHERE created_at >= NOW() - (months || ' months')::INTERVAL
            GROUP BY week, os
            ORDER BY week ASC, os
        ) t
    );
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;
```

---

## Step 6: Shyft AI Website Integration

### 6.1 Supabase Client Setup

Install the Supabase JS client:

```bash
npm install @supabase/supabase-js
```

Create a client module:

```typescript
// lib/supabase.ts
import { createClient } from "@supabase/supabase-js";

// These are safe to expose -- RLS restricts access to read-only
const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL!;
const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!;

export const supabase = createClient(supabaseUrl, supabaseAnonKey);
```

Environment variables (in `.env.local`):

```
NEXT_PUBLIC_SUPABASE_URL=https://<project-ref>.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...
```

### 6.2 API Routes (Next.js App Router)

Create API routes that the dashboard page calls. These server-side routes can cache responses.

```typescript
// app/api/dashboard/stats/route.ts
import { supabase } from "@/lib/supabase";
import { NextResponse } from "next/server";

export const revalidate = 300; // cache for 5 minutes

export async function GET() {
  const { data, error } = await supabase.rpc("get_dashboard_stats");

  if (error) {
    return NextResponse.json({ error: error.message }, { status: 500 });
  }

  return NextResponse.json(data);
}
```

```typescript
// app/api/dashboard/installs-by-os/route.ts
import { supabase } from "@/lib/supabase";
import { NextResponse } from "next/server";

export const revalidate = 300;

export async function GET() {
  const { data, error } = await supabase.rpc("get_installs_by_os");

  if (error) {
    return NextResponse.json({ error: error.message }, { status: 500 });
  }

  return NextResponse.json(data);
}
```

```typescript
// app/api/dashboard/trend/route.ts
import { supabase } from "@/lib/supabase";
import { NextResponse } from "next/server";

export const revalidate = 300;

export async function GET(request: Request) {
  const { searchParams } = new URL(request.url);
  const months = parseInt(searchParams.get("months") || "6");

  const { data, error } = await supabase.rpc("get_install_trend", { months });

  if (error) {
    return NextResponse.json({ error: error.message }, { status: 500 });
  }

  return NextResponse.json(data);
}
```

```typescript
// app/api/dashboard/companies/route.ts
import { supabase } from "@/lib/supabase";
import { NextResponse } from "next/server";

export const revalidate = 300;

export async function GET() {
  const { data, error } = await supabase
    .from("companies")
    .select("name, email_domain, install_count, os_frameworks, first_seen, last_seen")
    .order("install_count", { ascending: false })
    .limit(50);

  if (error) {
    return NextResponse.json({ error: error.message }, { status: 500 });
  }

  return NextResponse.json(data);
}
```

### 6.3 Dashboard Page Component

```tsx
// app/dashboard/page.tsx
import { Suspense } from "react";
import { StatsCards } from "@/components/dashboard/stats-cards";
import { InstallsByOSChart } from "@/components/dashboard/installs-by-os-chart";
import { TrendChart } from "@/components/dashboard/trend-chart";
import { CompaniesTable } from "@/components/dashboard/companies-table";

export default function DashboardPage() {
  return (
    <div className="space-y-8 p-8">
      <h1 className="text-3xl font-bold">Antigravity OS Dashboard</h1>

      <Suspense fallback={<div>Loading stats...</div>}>
        <StatsCards />
      </Suspense>

      <div className="grid grid-cols-1 lg:grid-cols-2 gap-8">
        <Suspense fallback={<div>Loading chart...</div>}>
          <InstallsByOSChart />
        </Suspense>

        <Suspense fallback={<div>Loading trend...</div>}>
          <TrendChart />
        </Suspense>
      </div>

      <Suspense fallback={<div>Loading companies...</div>}>
        <CompaniesTable />
      </Suspense>
    </div>
  );
}
```

```tsx
// components/dashboard/stats-cards.tsx
"use client";

import { useEffect, useState } from "react";

interface Stats {
  total_installs: number;
  this_week: number;
  this_month: number;
  unique_companies: number;
  unique_users: number;
  waitlist_count: number;
  frameworks_active: number;
}

export function StatsCards() {
  const [stats, setStats] = useState<Stats | null>(null);

  useEffect(() => {
    fetch("/api/dashboard/stats")
      .then((r) => r.json())
      .then(setStats);
  }, []);

  if (!stats) return <div>Loading...</div>;

  const cards = [
    { label: "Total Installs", value: stats.total_installs },
    { label: "This Week", value: stats.this_week },
    { label: "This Month", value: stats.this_month },
    { label: "Companies", value: stats.unique_companies },
    { label: "Unique Users", value: stats.unique_users },
    { label: "Waitlist", value: stats.waitlist_count },
    { label: "Frameworks Active", value: `${stats.frameworks_active}/8` },
  ];

  return (
    <div className="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-7 gap-4">
      {cards.map((card) => (
        <div
          key={card.label}
          className="bg-white dark:bg-gray-800 rounded-lg p-4 shadow-sm border"
        >
          <div className="text-2xl font-bold">{card.value}</div>
          <div className="text-sm text-gray-500">{card.label}</div>
        </div>
      ))}
    </div>
  );
}
```

```tsx
// components/dashboard/installs-by-os-chart.tsx
"use client";

import { useEffect, useState } from "react";
// Use any chart library: recharts, chart.js, etc.
// Example with recharts:
// import { PieChart, Pie, Cell, Tooltip, Legend } from "recharts";

interface OsData {
  os: string;
  installs: number;
  percentage: number;
}

const OS_COLORS: Record<string, string> = {
  gtmos: "#3B82F6",      // blue
  csos: "#10B981",       // green
  contentos: "#F59E0B",  // amber
  financeos: "#6366F1",  // indigo
  hros: "#EC4899",       // pink
  investoros: "#8B5CF6",  // purple
  communityos: "#14B8A6", // teal
  founderos: "#F97316",  // orange
};

const OS_LABELS: Record<string, string> = {
  gtmos: "GTM:OS",
  csos: "CS:OS",
  contentos: "CONTENT:OS",
  financeos: "FINANCE:OS",
  hros: "HR:OS",
  investoros: "INVESTOR:OS",
  communityos: "COMMUNITY:OS",
  founderos: "FOUNDER:OS",
};

export function InstallsByOSChart() {
  const [data, setData] = useState<OsData[]>([]);

  useEffect(() => {
    fetch("/api/dashboard/installs-by-os")
      .then((r) => r.json())
      .then((d) => setData(d || []));
  }, []);

  if (!data.length) return <div>No data yet</div>;

  // Render with your preferred chart library
  // This is a simple table fallback:
  return (
    <div className="bg-white dark:bg-gray-800 rounded-lg p-6 shadow-sm border">
      <h2 className="text-lg font-semibold mb-4">Installs by Framework</h2>
      <div className="space-y-2">
        {data.map((item) => (
          <div key={item.os} className="flex items-center gap-3">
            <div
              className="w-3 h-3 rounded-full"
              style={{ backgroundColor: OS_COLORS[item.os] }}
            />
            <span className="w-28 text-sm font-medium">
              {OS_LABELS[item.os] || item.os}
            </span>
            <div className="flex-1 bg-gray-100 dark:bg-gray-700 rounded-full h-4">
              <div
                className="h-4 rounded-full"
                style={{
                  width: `${item.percentage}%`,
                  backgroundColor: OS_COLORS[item.os],
                }}
              />
            </div>
            <span className="text-sm text-gray-500 w-20 text-right">
              {item.installs} ({item.percentage}%)
            </span>
          </div>
        ))}
      </div>
    </div>
  );
}
```

```tsx
// components/dashboard/companies-table.tsx
"use client";

import { useEffect, useState } from "react";

interface Company {
  name: string;
  email_domain: string;
  install_count: number;
  os_frameworks: string[];
  first_seen: string;
  last_seen: string;
}

const OS_LABELS: Record<string, string> = {
  gtmos: "GTM", csos: "CS", contentos: "CONTENT",
  financeos: "FINANCE", hros: "HR", investoros: "INVESTOR",
  communityos: "COMMUNITY", founderos: "FOUNDER",
};

export function CompaniesTable() {
  const [companies, setCompanies] = useState<Company[]>([]);

  useEffect(() => {
    fetch("/api/dashboard/companies")
      .then((r) => r.json())
      .then((d) => setCompanies(d || []));
  }, []);

  if (!companies.length) return <div>No companies registered yet</div>;

  return (
    <div className="bg-white dark:bg-gray-800 rounded-lg p-6 shadow-sm border">
      <h2 className="text-lg font-semibold mb-4">Companies</h2>
      <div className="overflow-x-auto">
        <table className="w-full text-sm">
          <thead>
            <tr className="border-b text-left">
              <th className="pb-2 font-medium">Company</th>
              <th className="pb-2 font-medium">Domain</th>
              <th className="pb-2 font-medium">Installs</th>
              <th className="pb-2 font-medium">Frameworks</th>
              <th className="pb-2 font-medium">First Seen</th>
              <th className="pb-2 font-medium">Last Seen</th>
            </tr>
          </thead>
          <tbody>
            {companies.map((c) => (
              <tr key={c.name} className="border-b">
                <td className="py-2 font-medium">{c.name}</td>
                <td className="py-2 text-gray-500">{c.email_domain}</td>
                <td className="py-2">{c.install_count}</td>
                <td className="py-2">
                  <div className="flex gap-1 flex-wrap">
                    {c.os_frameworks.map((os) => (
                      <span
                        key={os}
                        className="px-1.5 py-0.5 text-xs rounded bg-gray-100 dark:bg-gray-700"
                      >
                        {OS_LABELS[os] || os}
                      </span>
                    ))}
                  </div>
                </td>
                <td className="py-2 text-gray-500">
                  {new Date(c.first_seen).toLocaleDateString()}
                </td>
                <td className="py-2 text-gray-500">
                  {new Date(c.last_seen).toLocaleDateString()}
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
}
```

---

## Step 7: Slack Notifications

### Setup

1. Go to https://api.slack.com/apps -- create a new app (or use existing)
2. Enable "Incoming Webhooks"
3. Add a webhook to your target channel (e.g., `#antigravity-installs`)
4. Copy the webhook URL

### Environment Configuration

Set the webhook URL as a Supabase edge function secret:

```bash
supabase secrets set SLACK_WEBHOOK_URL="https://hooks.slack.com/services/T.../B.../..."
```

### Message Formats

The edge functions already include Slack notification code. The messages sent are:

**Registration:**
```
New install: GTM:OS v1.4.0 by Acme Corp (jane@acme.com)
```

**Waitlist:**
```
Waitlist: Acme Corp interested in Enterprise tier for CS:OS
```

### Rich Message Format (optional upgrade)

Replace the simple text message with a Block Kit message for richer formatting:

```typescript
// Rich Slack message for registrations
const slackPayload = {
  blocks: [
    {
      type: "header",
      text: { type: "plain_text", text: "New OS Installation" },
    },
    {
      type: "section",
      fields: [
        { type: "mrkdwn", text: `*Framework:*\n${osDisplay[os]}` },
        { type: "mrkdwn", text: `*Version:*\nv${version}` },
        { type: "mrkdwn", text: `*Company:*\n${company}` },
        { type: "mrkdwn", text: `*Email:*\n${email}` },
      ],
    },
    {
      type: "context",
      elements: [
        { type: "mrkdwn", text: `Workspace: ${workspace} | ${new Date().toISOString()}` },
      ],
    },
  ],
};
```

---

## Step 8: Future Expansion

### 8.1 Heartbeat Endpoint

For tracking active usage. Each OS framework would POST periodically (e.g., on startup or daily).

**Endpoint:** `POST hooks.shyftai.com/heartbeat`

**Payload:**
```json
{
  "os": "gtmos",
  "version": "1.4.0",
  "workspace": "acme",
  "event": "session_start",
  "commands_used": ["gtm:pipeline", "gtm:health"],
  "timestamp": "ISO 8601"
}
```

This would insert into `usage_events` with `event_type = 'heartbeat'` and store `commands_used` in the `metadata` JSONB field.

### 8.2 Version Update Notifications

When a new version is released, query `installations` to find users on older versions. Could POST to a notification endpoint or send emails via Resend/SendGrid.

```sql
-- Find users on outdated versions
SELECT DISTINCT email, company, os, version
FROM installations i1
WHERE version < (
    SELECT MAX(version) FROM installations i2 WHERE i2.os = i1.os
)
ORDER BY os, company;
```

### 8.3 Feature Flags

Add a `feature_flags` table:

```sql
CREATE TABLE feature_flags (
    id          UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    flag_name   TEXT NOT NULL,
    os          TEXT,                    -- null = all OS frameworks
    company     TEXT,                    -- null = all companies
    enabled     BOOLEAN DEFAULT false,
    metadata    JSONB DEFAULT '{}',
    created_at  TIMESTAMPTZ DEFAULT NOW(),
    updated_at  TIMESTAMPTZ DEFAULT NOW(),

    UNIQUE(flag_name, os, company)
);
```

Edge function endpoint: `GET hooks.shyftai.com/flags?os=gtmos&company=acme`

### 8.4 Usage Analytics

Add command tracking to each OS framework. On each command execution, POST:

```json
{
  "os": "csos",
  "command": "cs:health-check",
  "workspace": "acme",
  "duration_ms": 1234,
  "timestamp": "ISO 8601"
}
```

Dashboard query for most popular commands:

```sql
SELECT
    os,
    event_name AS command,
    COUNT(*) AS executions,
    AVG((metadata->>'duration_ms')::INTEGER) AS avg_duration_ms
FROM usage_events
WHERE event_type = 'command'
GROUP BY os, event_name
ORDER BY executions DESC
LIMIT 20;
```

---

## Deploying the Edge Functions

### Local development

```bash
# Initialize Supabase in your project (if not done)
supabase init

# Create the function directories
supabase functions new register
supabase functions new waitlist

# Copy the TypeScript code from this briefing into:
#   supabase/functions/register/index.ts
#   supabase/functions/waitlist/index.ts

# Start local Supabase
supabase start

# Run the migration
supabase db reset  # applies all migrations

# Test locally
supabase functions serve register --env-file .env.local
```

### Deploy to production

```bash
# Set secrets
supabase secrets set SLACK_WEBHOOK_URL="https://hooks.slack.com/services/..."

# Deploy functions
supabase functions deploy register
supabase functions deploy waitlist

# Run migration on production
supabase db push
```

### Environment variables needed in Supabase

| Variable | Where to get it | Used by |
|----------|----------------|---------|
| `SUPABASE_URL` | Supabase project settings | Auto-available in edge functions |
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase project settings > API | Auto-available in edge functions |
| `SLACK_WEBHOOK_URL` | Slack app > Incoming Webhooks | Set via `supabase secrets set` |

---

## Testing Checklist

### Schema Verification

- [ ] Run migration without errors
- [ ] All tables created: `installations`, `companies`, `usage_events`, `waitlist`, `rate_limits`
- [ ] All views created: `installs_by_os`, `installs_by_week`, `company_os_matrix`, `installs_daily`, `version_distribution`, `waitlist_summary`
- [ ] All functions created: `check_rate_limit`, `upsert_company`, `cleanup_rate_limits`, `get_dashboard_stats`, `get_installs_by_os`, `get_install_trend`
- [ ] RLS enabled on all tables
- [ ] RLS policies allow service_role INSERT and anon SELECT

### Edge Function: /register

```bash
# Valid registration
curl -X POST https://hooks.shyftai.com/register \
  -H "Content-Type: application/json" \
  -d '{
    "os": "gtmos",
    "version": "1.4.0",
    "company": "Test Corp",
    "email": "test@testcorp.com",
    "workspace": "test-workspace",
    "timestamp": "2026-03-09T12:00:00Z"
  }'
# Expected: {"status":"registered"}

# Missing required field
curl -X POST https://hooks.shyftai.com/register \
  -H "Content-Type: application/json" \
  -d '{"os": "gtmos", "version": "1.4.0"}'
# Expected: {"error":"Missing required fields","fields":["company","email","timestamp"]}

# Invalid OS
curl -X POST https://hooks.shyftai.com/register \
  -H "Content-Type: application/json" \
  -d '{
    "os": "invalid",
    "version": "1.0.0",
    "company": "Test",
    "email": "test@test.com",
    "workspace": "test",
    "timestamp": "2026-03-09T12:00:00Z"
  }'
# Expected: {"error":"Invalid OS framework","valid_values":[...]}

# Invalid email
curl -X POST https://hooks.shyftai.com/register \
  -H "Content-Type: application/json" \
  -d '{
    "os": "gtmos",
    "version": "1.0.0",
    "company": "Test",
    "email": "not-an-email",
    "workspace": "test",
    "timestamp": "2026-03-09T12:00:00Z"
  }'
# Expected: {"error":"Invalid email format"}

# Invalid version
curl -X POST https://hooks.shyftai.com/register \
  -H "Content-Type: application/json" \
  -d '{
    "os": "gtmos",
    "version": "abc",
    "company": "Test",
    "email": "test@test.com",
    "workspace": "test",
    "timestamp": "2026-03-09T12:00:00Z"
  }'
# Expected: {"error":"Invalid version format. Expected: X.Y.Z"}

# Rate limiting (send 11+ requests quickly)
for i in $(seq 1 12); do
  curl -s -X POST https://hooks.shyftai.com/register \
    -H "Content-Type: application/json" \
    -d "{
      \"os\": \"gtmos\",
      \"version\": \"1.0.0\",
      \"company\": \"RateTest\",
      \"email\": \"rate${i}@test.com\",
      \"workspace\": \"test\",
      \"timestamp\": \"2026-03-09T12:00:00Z\"
    }"
  echo ""
done
# Expected: first 10 return 200, 11th+ return 429
```

### Edge Function: /waitlist

```bash
# Valid waitlist signup
curl -X POST https://hooks.shyftai.com/waitlist \
  -H "Content-Type: application/json" \
  -d '{
    "email": "team@acme.com",
    "company": "Acme Corp",
    "os": "csos",
    "tier_interest": "team"
  }'
# Expected: {"status":"waitlisted"}

# Invalid tier
curl -X POST https://hooks.shyftai.com/waitlist \
  -H "Content-Type: application/json" \
  -d '{
    "email": "team@acme.com",
    "company": "Acme Corp",
    "os": "csos",
    "tier_interest": "free"
  }'
# Expected: {"error":"Invalid tier. Must be: team, business, or enterprise"}
```

### Data Integrity

- [ ] Registration creates row in `installations`
- [ ] First registration from a company creates row in `companies`
- [ ] Second registration from same company updates `install_count`, `last_seen`, appends to `os_frameworks` and `emails`
- [ ] `companies.os_frameworks` does not contain duplicates
- [ ] `companies.emails` does not contain duplicates
- [ ] Dashboard stats RPC returns correct counts
- [ ] Views return expected data shapes

### Slack Notifications

- [ ] Registration triggers Slack message in configured channel
- [ ] Waitlist signup triggers Slack message
- [ ] Message format is readable and contains all key fields
- [ ] Missing `SLACK_WEBHOOK_URL` does not cause errors (fails silently)

### DNS / Routing

- [ ] `hooks.shyftai.com/register` resolves and returns 200 for valid POST
- [ ] `hooks.shyftai.com/waitlist` resolves and returns 200 for valid POST
- [ ] CORS preflight (OPTIONS) returns 200 with correct headers
- [ ] Non-POST methods return 405
- [ ] Unknown paths return 404

### Dashboard

- [ ] Stats cards load and display correct numbers
- [ ] Installs by OS chart renders
- [ ] Trend chart renders with weekly data
- [ ] Companies table loads and sorts by install count
- [ ] Data refreshes (not stale beyond 5-minute cache)

---

## Monitoring and Alerts

### Supabase Dashboard

- Monitor edge function invocations in Supabase Dashboard > Edge Functions
- Check error rates and latency
- Set up database webhooks for anomaly detection

### Recommended Alerts

1. **Error rate spike:** If edge function error rate exceeds 5% in 5 minutes
2. **Rate limit triggers:** Monitor rate_limits table for unusual activity
3. **New company registration:** Already handled via Slack
4. **Database size:** Monitor row counts approaching free tier limits

### Supabase Free Tier Limits (as of 2026)

| Resource | Limit | Monitor |
|----------|-------|---------|
| Database size | 500 MB | `SELECT pg_database_size(current_database())` |
| Edge function invocations | 500K/month | Supabase dashboard |
| Bandwidth | 5 GB/month | Supabase dashboard |
| Rows in tables | No hard limit | Row count queries |

### Cleanup Job

Set up a scheduled function or cron to clean up rate limit entries:

```sql
-- Run daily via pg_cron or a scheduled edge function
SELECT cleanup_rate_limits();
```

---

## Quick Reference: File Inventory

When implementation is complete, these files should exist:

```
supabase/
  migrations/
    001_registration_schema.sql     # Database schema
  functions/
    register/
      index.ts                      # Registration edge function
    waitlist/
      index.ts                      # Waitlist edge function

# If using Cloudflare Worker (Option A):
cloudflare-worker/
  wrangler.toml                     # Worker config
  src/
    index.js                        # Router

# Shyft AI website additions:
lib/
  supabase.ts                       # Supabase client
app/
  api/
    dashboard/
      stats/route.ts                # Dashboard stats API
      installs-by-os/route.ts       # Pie chart data API
      trend/route.ts                # Trend chart data API
      companies/route.ts            # Companies list API
  dashboard/
    page.tsx                        # Dashboard page
components/
  dashboard/
    stats-cards.tsx                  # Stats cards component
    installs-by-os-chart.tsx        # OS distribution chart
    trend-chart.tsx                 # Weekly trend chart
    companies-table.tsx             # Companies table
```

---

## Appendix: Updating OS Framework Onboard Commands

Each OS framework's onboard command already POSTs to `https://hooks.shyftai.com/register`. No changes needed to the payload format. The edge function accepts the exact payload structure already in use.

If switching to direct Supabase URL (Option C) during development, update the URL in these files:

| File | Line |
|------|------|
| `CSOS/.claude/commands/cs/onboard.md` | ~85 |
| `FINANCEOS/.claude/commands/finance/onboard.md` | ~33 |
| `CONTENTOS/.claude/commands/content/onboard.md` | ~64 |
| `HROS/.claude/commands/hr/onboard.md` | ~32 |
| `COMMUNITYOS/.claude/commands/community/onboard.md` | ~17 |
| `FOUNDEROS/.claude/commands/founder/onboard.md` | ~24 |
| `GTMOS` | Check for onboard command |
| `INVESTOROS` | Check for onboard command |

For production, keep `hooks.shyftai.com/register` as the canonical URL.
