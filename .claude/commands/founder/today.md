---
name: founder:today
description: Daily founder cockpit — everything across all frameworks
argument-hint: "<workspace-name>"
---
<objective>
The founder's daily cockpit. Pulls key data from ALL connected OS frameworks into one view.

Workspace: $ARGUMENTS
</objective>

<execution_context>
@./.claude/founderos/references/defaults.md
</execution_context>

<process>
1. Display: `<< FOUNDER:OS // TODAY >>`
2. Load workspace context — PRIORITIES.md, OKRS.md, DECISIONS.md, ENERGY.md
3. Detect connected OS frameworks by checking /c/Antigravity/{GTMOS,CONTENTOS,FINANCEOS,HROS,INVESTOROS,COMMUNITYOS,CSOS}

## Priorities
4. Show today's top 3 priorities from PRIORITIES.md
5. Show OKR progress — current quarter key results with % complete

## Cross-framework pulse
6. Pull key signals from each connected framework:

**Money** (FINANCE:OS)
- Cash position and runway
- Burn rate trend
- Overdue invoices or bills

**Revenue** (GTM:OS)
- Pipeline value and meetings today
- Active campaigns and reply rate
- Deals close to closing

**Team** (HR:OS)
- Open roles and hiring pipeline
- Pending offers
- Reviews or PIPs due

**Fundraising** (INVESTOR:OS)
- Round status and pipeline stage
- Follow-ups due today
- Term sheets in play

**Content** (CONTENT:OS)
- Content publishing today
- Top performing content
- Engagement metrics

**Community** (COMMUNITY:OS)
- Engagement rate and new members
- Events today
- At-risk members

**Customer Success** (CS:OS)
- Net revenue retention (NRR)
- At-risk customers count and ARR at risk
- Upcoming renewals this month
- NPS score and trend
- Expansion pipeline value

7. For each framework: only show if the directory exists. Skip gracefully if not connected.

## Decisions pending
8. Show open decisions from DECISIONS.md that need resolution

## Energy plan
9. Show today's schedule from ENERGY.md:
   - Deep work blocks
   - Meeting blocks
   - Buffer time

## Alerts
10. Flag critical items across all frameworks:
    - Runway < 6 months
    - Expiring offers
    - Overdue follow-ups (investor)
    - Budget overages
    - Compliance deadlines

## Actions
11. Suggest top 3 actions for today based on:
    - Urgency (deadlines, overdue items)
    - OKR impact (which action moves key results most)
    - Energy alignment (match action to current energy block)

12. Display:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Route to:
  >> /gtm:today — deep dive into sales
  >> /finance:today — deep dive into money
  >> /hr:today — deep dive into team
  >> /investor:today — deep dive into fundraising
  >> /content:today — deep dive into content
  >> /community:today — deep dive into community
  >> /cs:today — deep dive into customer success

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```
</process>
