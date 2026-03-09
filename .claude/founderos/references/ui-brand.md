<ui_patterns>

Visual patterns for user-facing FOUNDER:OS output. All commands @-reference this file.

## Brand Color

FOUNDER:OS brand color is **gold/amber** (ANSI 220).
- Use `\033[38;5;220m` to set gold text, `\033[0m` to reset
- Apply gold to: the FOUNDER:OS block-letter banner, mode headers (`<< FOUNDER:OS // MODE >>`), section titles in dashboards
- Use white/default for: body text, data values, box borders
- If terminal doesn't support color, display everything in plain white
- Never use orange (that's GTM:OS), blue (CONTENT:OS), green (FINANCE:OS), or cyan (COMMUNITY:OS)

## Startup Banner

Display once when FOUNDER:OS loads. Render the block letters in gold.

```
███████╗ ██████╗ ██╗   ██╗███╗   ██╗██████╗ ███████╗██████╗  ██╗  ██████╗ ███████╗
██╔════╝██╔═══██╗██║   ██║████╗  ██║██╔══██╗██╔════╝██╔══██╗ ╚═╝ ██╔═══██╗██╔════╝
█████╗  ██║   ██║██║   ██║██╔██╗ ██║██║  ██║█████╗  ██████╔╝     ██║   ██║███████╗
██╔══╝  ██║   ██║██║   ██║██║╚██╗██║██║  ██║██╔══╝  ██╔══██╗ ██╗ ██║   ██║╚════██║
██║     ╚██████╔╝╚██████╔╝██║ ╚████║██████╔╝███████╗██║  ██║ ╚═╝ ╚██████╔╝███████║
╚═╝      ╚═════╝  ╚═════╝ ╚═╝  ╚═══╝╚═════╝ ╚══════╝╚═╝  ╚═╝     ╚═════╝ ╚══════╝
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  F O U N D E R : O S
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Mode Headers

Use for workflow transitions. FOUNDER:OS uses angle brackets.

```
<< FOUNDER:OS // {MODE NAME} >>
```

**Mode names (uppercase, rendered in gold):**
- `ONBOARDING`
- `TODAY`
- `DASHBOARD`
- `WEEKLY REVIEW`
- `OKRs`
- `DECIDE`
- `DELEGATE`
- `PRIORITIES`
- `VISION`
- `STRATEGY`
- `PIVOT ANALYSIS`
- `BOARD UPDATE`
- `INVESTOR UPDATE`
- `HIRE`
- `FUNDRAISE`
- `ENERGY`
- `NETWORK`
- `RISKS`
- `LAUNCH`
- `METRICS`
- `REPORT`
- `DEBRIEF`
- `REVIEW`
- `STATUS`
- `FEEDBACK`

---

## Workspace Header

Show after loading a workspace.

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  WORKSPACE: {Company Name}                                  ┃
┃  Stage: {stage}    Team: {size}    Role: {role}             ┃
┃  North star: {metric} = {current value}                     ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

---

## Approval Gates

**Interactive mode:**
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  APPROVAL REQUIRED                                          ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

{What is being approved}

>> Approve / Edit / Reject
```

**Hard gates (always stop, even in auto mode):**
- Board communications
- Investor communications
- Hiring/firing decisions
- Fundraising decisions
- Public announcements

---

## Decision Gates Display

```
  ── DECISION GATES ──────────────────────────────────
  [x] Vision       [x] OKR impact    [x] Data backed
  [x] Reversible   [x] Delegation    [x] Energy
  ─────────────────────────────────────────────────
```

---

## Status Symbols

```
[x]  Passed / Complete / Connected
[ ]  Failed / Missing / Not connected
[~]  Borderline / Needs review
>>   Action prompt — waiting for human input
!!   Warning or urgent flag
--   Skipped / Not applicable
```

---

## Next Action Block

Always at end of a completed workflow.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> Next: {suggested next command}
     Also: {alternative command}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Anti-Patterns — What FOUNDER:OS never does

- Never use GTM:OS orange (`\033[38;5;208m`) — that's their brand
- Never use `GSD` prefix — that's GSD's brand
- Never use random emoji (no rockets, sparkles, stars)
- Never vary box widths within the same output
- Never show data without labeling which OS framework it came from
- Never present a dashboard with invented numbers — always pull from source

</ui_patterns>
