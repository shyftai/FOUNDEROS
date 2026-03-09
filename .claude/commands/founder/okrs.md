Set, track, and review OKRs. Load `.claude/founderos/references/okr-guide.md` before running.

Display:
```
<< FOUNDER:OS // OKRs >>
```

Follow these steps based on the sub-command:

**Set new OKRs (/founder:okrs set):**
1. Ask: "What quarter are we setting OKRs for?"
2. Review the company vision from VISION.md — OKRs must serve the vision
3. Ask for 2-3 objectives — these should be qualitative, inspiring, and ambitious
4. For each objective, ask for 2-3 key results — these must be measurable with a specific number
5. Validate each key result: Is it measurable? Is it ambitious but achievable (target 0.6-0.7 score)? Does it have a clear owner?
6. Check that OKRs collectively cover the company's top priorities
7. Run the OKR health check:
   - [ ] Each objective is qualitative and inspiring
   - [ ] Each key result is measurable with a number
   - [ ] 3-5 key results per objective maximum
   - [ ] At least one KR per objective is a stretch
   - [ ] Every KR has a clear owner
   - [ ] OKRs align with vision
8. Save to OKRS.md
9. Suggest which OKRs map to which connected OS framework

**Track OKRs (/founder:okrs track):**
1. Read current OKRS.md
2. Pull relevant data from connected OS frameworks to update key result progress
3. Calculate scores (0.0-1.0) for each key result
4. Flag any key results that are at risk (below expected progress for this point in the quarter)
5. Display the OKR scorecard with progress bars
6. Suggest actions to get at-risk KRs back on track
7. Update OKRS.md with current scores

**Review OKRs (/founder:okrs review):**
1. Score each key result final (0.0-1.0)
2. Calculate average score per objective and overall
3. For each KR: was the target right? Too easy (scored 1.0)? Too hard (scored <0.3)?
4. Extract learnings about goal-setting quality
5. Identify which OKRs to carry forward, modify, or retire
6. Log learnings to LEARNINGS.md
7. Display the quarter review:

```
  ┌─ OKR REVIEW — {Quarter} ────────────────────────────────┐
  │                                                          │
  │  Average score: {0.X}  (target: 0.6-0.7)                │
  │                                                          │
  │  O1: {objective}     Score: {0.X}                        │
  │    KR1: {0.X}  KR2: {0.X}  KR3: {0.X}                  │
  │                                                          │
  │  O2: {objective}     Score: {0.X}                        │
  │    KR1: {0.X}  KR2: {0.X}                               │
  │                                                          │
  │  Key learning: {what we learned about goal-setting}      │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

8. Prompt to set next quarter's OKRs: `/founder:okrs set`
