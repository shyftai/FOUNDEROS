# Notifications

Slack alert configuration for FOUNDER:OS. Requires Slack MCP and `slack_enabled: true` in global/COLLABORATION.md.

---

## Alert triggers

### Critical (immediate)

| Trigger | Message format | Channel |
|---------|---------------|---------|
| Cash runway below 6 months | "!! RUNWAY ALERT: {months} months remaining at current burn of ${burn}/mo" | #founder-alerts |
| Key hire rejected offer | "!! OFFER DECLINED: {name} for {role} — reason: {reason}" | #founder-alerts |
| Revenue dropped >20% MoM | "!! REVENUE DROP: MRR fell {%} from ${prev} to ${current}" | #founder-alerts |
| Critical risk triggered | "!! RISK TRIGGERED: {risk description}" | #founder-alerts |

### High (same day)

| Trigger | Message format | Channel |
|---------|---------------|---------|
| OKR at risk (>20% behind target) | "! OKR AT RISK: {KR description} — {current} vs {target} ({score})" | #founder-alerts |
| Board meeting in 7 days | "! BOARD PREP: Board meeting in 7 days. Materials due in {n} days." | #founder-alerts |
| Investor update overdue | "! INVESTOR UPDATE: Last update was {n} days ago. Due by {date}." | #founder-alerts |
| Key hire accepted offer | "Key hire accepted: {name} for {role}, starting {date}" | #founder-alerts |

### Medium (next check-in)

| Trigger | Message format | Channel |
|---------|---------------|---------|
| Decision deadline approaching | "Decision D-{id} due in {n} days: {title}" | #founder-alerts |
| Delegation overdue | "Delegation overdue: {task} assigned to {person}, due {date}" | #founder-alerts |
| Weekly review not completed | "Weekly review not completed this week" | #founder-alerts |
| Deep work target missed | "Deep work: {actual}h vs {target}h target this week" | #founder-alerts |

### Informational

| Trigger | Message format | Channel |
|---------|---------------|---------|
| OKR milestone hit | "OKR milestone: {KR description} reached {score}" | #founder-wins |
| Revenue milestone | "Revenue milestone: MRR passed ${amount}" | #founder-wins |
| Team milestone | "Team: {name} started as {role}" | #founder-wins |
| Decision reviewed | "Decision D-{id} reviewed: {outcome}" | #founder-alerts |

---

## Notification rules

1. **Critical alerts** — send immediately, regardless of time
2. **High alerts** — send during working hours (9am-6pm founder timezone)
3. **Medium alerts** — batch and send at next check-in (/founder:today)
4. **Informational** — send to #founder-wins channel, not #founder-alerts
5. **Duplicates** — never send the same alert twice within 24 hours
6. **Quiet hours** — no alerts between 9pm-7am except critical

---

## Fallback behavior

If Slack is not connected, display notifications inline with `!!` prefix during /founder:today or /founder:dashboard. Never suppress critical alerts — always surface them.
