# FOUNDER:OS — Collaboration Mode

## Current mode

**Mode:** solo

---

## Solo mode (default)

All state lives in markdown files. No database needed. One operator per workspace. Best for solo founders and small teams.

## Team mode (optional)

Shared state syncs via Supabase. Enables:
- Shared decision log (multiple founders/C-suite can log decisions)
- Real-time OKR progress tracking across team members
- Delegation tracking with assignee notifications
- Shared risk register
- Activity feed (who decided what when)

**To enable:**
1. Create a Supabase project
2. Add SUPABASE_URL and SUPABASE_ANON_KEY to `.env`
3. Set mode to `team` in this file

**Dual-write rule:** In team mode, always write to both Supabase AND the local markdown file. Markdown is the cache. Supabase is the source of truth.

**Fallback rule:** If Supabase is unreachable, fall back to file-based mode. Warn the user. Never block work because of a connection issue.

---

## Slack notifications

**Slack enabled:** false
**Slack channel:** #founder-alerts

When enabled, send alerts for:
- OKR at risk (>20% behind target)
- Cash runway below 6 months
- Key hire accepted/rejected offer
- Board meeting in 7 days
- Investor update overdue
- Decision deadline approaching
