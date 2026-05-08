<!--
================================================================================
HOW THE AAR DRAFTER USES THIS FILE
================================================================================

This file is the SHAPE of an AAR. The drafter reads the filled forms from a
completed tabletop exercise and substitutes scenario-specific findings into the
template below. Read the bullets and the severity rubric before drafting.
Anything outside the literal template (the part below the second double-rule
divider) is guidance for you, the drafter — do not include it in the output.

## Substitution rules

- `{{placeholders}}` are slots. Replace with concrete content drawn from the
  forms. Never leave a placeholder unfilled in the final AAR — if you genuinely
  don't have the info, write `Unknown — facilitator did not capture` so the gap
  is visible rather than hidden.
- `<!-- drafter notes -->` are for you. Strip them from the final AAR.
- Section numbering is fixed. Do not renumber, reorder, or insert new top-level
  sections. Sub-section headings under §6 may be omitted if a category is empty
  (see §6 note), but the parent section stays.

## When the forms are mostly empty

If more than half the forms are blank, you've already warned the user per the
SKILL.md workflow. When drafting anyway:

- Write the scaffold faithfully, but mark thin sections with
  `> [!warning] Sparse evidence — facilitator captured limited notes during the
  > exercise. Findings below reflect only what was logged.`
- Do not invent decisions, timestamps, or attendees that weren't recorded.
  Better to ship a thin AAR honestly than a padded one with fabricated detail.
- Bias toward fewer, well-cited findings. A 3-bullet "what didn't go well" with
  real cites beats a 7-bullet list with three made-up ones.

## How `--audience` changes register

Same facts, different emphasis. The body of the AAR stays factual; tone and
elevation choices shift:

- `internal` — peers and adjacent teams. Plain language, jargon OK if the team
  uses it daily. Names of individuals fine in §3 timeline (e.g. "Priya
  escalated to on-call lead at 14:22"). Action items can reference internal
  ticketing systems by name.
- `leadership` (default) — VPs, directors. Lead with business impact in §1.
  Keep individual names but de-emphasize them in favor of roles. Translate
  technical jargon. Action items framed as commitments with owners and dates.
- `regulator` — external compliance audience (e.g. SEC, FCA, state AG, DPA).
  Anonymize attendees to roles only ("VP Eng", "Head of Legal"). Strip
  internal-only jargon. Stick to factual reconstruction; avoid speculative
  framing. Cite the exercise's regulatory hook explicitly in §2 if there is
  one (e.g. "exercise tested SEC Reg S-P §248.30 incident-response controls").
- `board` — directors, audit committee. Anonymize. Lead §1 with materiality
  framing. Keep §3 short — boards want findings and actions, not minute-by-
  minute reconstruction. Move detailed timeline to Appendix D and reference it.

## Section-by-section emphasis guidance

- **§1 Executive summary** — 3-5 sentences, hard cap. If you can't say what was
  tested, the top three takeaways, and the top three action items in five
  sentences, you don't understand the exercise yet. Re-read the forms.
- **§2 Exercise overview** — facts only, no judgment. Anonymize attendees if
  audience is `regulator` or `board`.
- **§3 Timeline** — factual reconstruction. Use the actual timestamps captured
  during the exercise, not the planned timing. No commentary; commentary lives
  in §4 and §5. Leadership/board: keep tight (~one short paragraph per phase).
  Internal/regulator: full granularity.
- **§4 What went well** — 4-7 bullets typically. Don't sandbag. If the team
  genuinely did well, say so plainly. Tie each bullet to a capability the
  exercise was designed to test (e.g. "validated escalation path to Legal
  within SLA").
- **§5 What didn't go well** — 4-7 bullets typically. BLAMELESS. Describe the
  system gap, not the individual. "Escalation hesitated for 11 minutes because
  decision rights between IR lead and Legal were ambiguous" — not "Sam
  hesitated to escalate." Every bullet cites a decision-log entry by
  timestamp.
- **§6 Gaps** — categorized findings with severity tags. Pull from §5 and the
  gaps form. Omit a sub-category entirely if no findings fall into it; do not
  pad with weak findings to "balance" categories.
- **§7 Action items** — 5-12 items typical. Fewer than 5 likely means the AAR
  is sandbagging. More than 12 means too granular — group related items.
  Every item has a real owner and a real deadline. If the facilitator didn't
  capture an owner, write `OWNER NEEDED` so the team has to assign before
  finalizing. Order P0 first, then P1, then P2.
- **§8 Recommendations for next exercise** — driven by the gaps surfaced this
  time. What's still untested? What format adjustments would help (was 90 min
  too short)? Who else should be in the room?
- **§9 Appendices** — embed raw form contents. Anonymize attendance if
  regulator/board.

## Severity rubric for action items (P0 / P1 / P2)

Use these criteria, not vibes. If you can't justify the severity against the
criteria, you've miscategorized.

- **P0** — would cause material harm if encountered in a real incident.
  Material means: financial loss, regulatory exposure, customer-trust damage,
  or life/safety risk. Fix in days, not weeks. Examples: cannot reach
  decision-maker on the critical path; no documented breach-notification
  process for a PII jurisdiction we operate in; runbook references a tool
  that's been decommissioned; no on-call rotation for a system that handles
  authentication.
- **P1** — significantly degrades real-incident response but workable around.
  Fix in weeks. Examples: runbook exists but is materially out of date;
  escalation path ambiguous between two roles; key tool not deployed in one
  region; comms templates exist but haven't been legal-reviewed.
- **P2** — friction that slows response but doesn't block it. Fix in current
  or next quarter. Examples: dashboard layout could be clearer; would be nice
  to have an automated severity classifier; runbook formatting inconsistent
  across services.

## Tone rules

- **Blameless.** Multiple times in this template you'll see this reminder.
  It is the single most important rule. Describe behavior in terms of system
  gaps, ambiguous ownership, missing tooling, or unclear playbooks — not
  individual fault. The exercise exists to surface system gaps; AARs that name
  and shame poison the next one.
- **Specific.** Every finding cites evidence — a decision-log entry by
  timestamp, an item from the gaps form, or a documented absence ("runbook
  contains no escalation path for after-hours legal contact"). "Communication
  could be improved" is not a finding; it's a vibe.
- **Honest.** If the team failed badly, say so plainly. Don't dress up a
  serious gap as a "growth opportunity." A regulator reading an AAR that
  sandbags real findings will trust your IR program less, not more.
- **Style anchor.** Write like a respected senior IR consultant: knowledgeable,
  direct, kind, unwilling to bullshit. Professional but warm. Not bureaucratic.

================================================================================
TEMPLATE BEGINS BELOW — everything below this line is the literal AAR shape
================================================================================
-->

# After-Action Report — {{scenario title}}

> **Date**: {{date}} · **Duration**: {{actual duration}} · **Audience**: {{audience}} · **Facilitator**: {{facilitator name}}
> AAR drafted {{aar-date}}

## 1. Executive summary

{{3-5 sentences max. State (a) what was tested, (b) who attended at high level — count + roles, not names unless internal audience, (c) the top 3 takeaways, (d) the top 3 action items by severity. Tune to audience: leadership leads with business impact; regulator leads with control coverage and findings against the regulatory hook; board leads with materiality.}}

<!-- drafter: hard cap 5 sentences. If you need 6, you haven't synthesized hard enough. Re-read §4-§7 and compress. -->

## 2. Exercise overview

- **Scenario**: {{name}} — {{1-line summary of the scenario premise}}
- **Objectives**: {{3-5 bullet objectives the exercise was designed to test, pulled from RUNBOOK.md}}
- **Attendees**: {{by role; include count. Anonymize names entirely if --audience is regulator or board. Internal/leadership may include names.}}
- **Duration**: {{planned duration}} planned · {{actual duration}} actual {{(note any material variance and why, if known)}}
- **Format**: {{in-person | hybrid | remote}}
- **Materials used**: {{which artifacts were referenced — RUNBOOK.html, forms, injects, external runbooks, etc.}}
- **Regulatory or framework hook** (if applicable): {{e.g. SEC Reg S-P §248.30, NIST IR-4, SOC2 CC7.3, GDPR Art. 33}}

<!-- drafter: omit the regulatory hook line if there isn't one — don't leave the placeholder. -->

## 3. Timeline reconstruction

<!-- drafter: phase-by-phase narrative built from forms/decision-log.md and forms/timeline-reconstruction.md. Use the ACTUAL timestamps captured during the exercise, not the planned timing from RUNBOOK.md. Stay factual — commentary belongs in §4 and §5. ~3-6 lines per phase. For board/leadership audiences keep tighter; for internal/regulator use full granularity. If timestamps are missing, mark "(time not captured)" rather than estimating. -->

### Phase 1 — {{phase name from RUNBOOK.md}}

{{Factual narrative: what the inject was, how the team responded, key decisions and who made them, what was escalated and to whom, with timestamps. Cite decision-log entries by their timestamp like (14:22) inline.}}

### Phase 2 — {{phase name}}

{{...}}

### Phase 3 — {{phase name}}

{{...}}

<!-- drafter: add as many phases as the exercise had. Don't invent phases that didn't happen. -->

## 4. What went well

<!-- drafter: 4-7 bullets typically. Each bullet: specific behavior + cite by timestamp + why it mattered. Tie each to a capability the exercise was designed to test (see §2 objectives). Don't sandbag — if the team genuinely did well, say so plainly. BLAMELESS framing applies here too: credit the system, not just the individual ("escalation path was clear and the on-call lead used it" rather than "Priya did a great job"). -->

- {{specific behavior or decision}} ({{timestamp cite}}) — {{why it mattered, tied to which exercise objective it validated}}
- {{...}}
- {{...}}

## 5. What didn't go well

<!-- drafter: 4-7 bullets typically. BLAMELESS — describe behavior as system gaps, not individual fault. Cite the decision log by timestamp. Each bullet must be a specific incident, not a generic vibe. Bad: "communication could be improved." Good: "escalation to Legal hesitated for 11 minutes (14:22-14:33) because decision rights between IR lead and Legal counsel were ambiguous in the current runbook." If the team failed badly somewhere, say so plainly — sandbagging here defeats the point of the exercise. -->

- {{specific behavior or hesitation}} ({{timestamp cite}}) — {{system gap that caused it: missing tooling, ambiguous ownership, undocumented escalation, etc.}}
- {{...}}
- {{...}}

## 6. Gaps identified

<!-- drafter: categorized findings pulled from §5 and forms/gaps-and-findings.md. Each gap = 1-line description + 1-line evidence cite + severity tag using the rubric at the top of this file. Omit a sub-section entirely if no findings fall into that category; do not pad to "balance" the categories. -->

### 6.1 Technical

<!-- missing tooling, alerting blind spots, runbook gaps, integration failures, monitoring coverage holes -->

- **{{gap description}}** [{{P0|P1|P2}}] — {{evidence cite from decision log timestamp or gaps form entry}}
- **{{...}}** [{{...}}] — {{...}}

### 6.2 Process

<!-- unclear ownership, escalation ambiguity, decision rights, playbook gaps, SLA undefined -->

- **{{gap description}}** [{{P0|P1|P2}}] — {{evidence cite}}
- **{{...}}** [{{...}}] — {{...}}

### 6.3 Communication

<!-- internal coordination breakdowns, customer/regulator/exec messaging gaps, comms-template absence, channel confusion -->

- **{{gap description}}** [{{P0|P1|P2}}] — {{evidence cite}}
- **{{...}}** [{{...}}] — {{...}}

### 6.4 People / training

<!-- knowledge gaps, single-points-of-knowledge, training overdue, role coverage thin, after-hours coverage gap -->

- **{{gap description}}** [{{P0|P1|P2}}] — {{evidence cite}}
- **{{...}}** [{{...}}] — {{...}}

## 7. Action items

<!-- drafter: ordered by severity (P0 first, then P1, then P2). Every item has a real owner and a real deadline — no "TBD". If the facilitator didn't capture an owner, write `OWNER NEEDED` so the team must assign before the doc is finalized. Tracking column is a placeholder for the team to fill in their ticket ID. Aim for 5-12 items. Fewer than 5 likely means the AAR is sandbagging the findings. More than 12 means you should group related items. Verb-led action phrasing ("Document …", "Deploy …", "Update …") — not noun phrases. -->

| # | Action | Owner | Severity | Target | Tracking |
|---|--------|-------|----------|--------|----------|
| 1 | {{specific verb-led action}} | {{name or role, or `OWNER NEEDED`}} | P0 | {{YYYY-MM-DD}} | {{ticket placeholder}} |
| 2 | {{...}} | {{...}} | P0 | {{...}} | {{...}} |
| 3 | {{...}} | {{...}} | P1 | {{...}} | {{...}} |
| 4 | {{...}} | {{...}} | P1 | {{...}} | {{...}} |
| 5 | {{...}} | {{...}} | P2 | {{...}} | {{...}} |

## 8. Recommendations for next exercise

<!-- drafter: 3-5 bullets. Driven by the gaps surfaced this time — what's still untested? Plus format adjustments (was 90 min too short? did certain roles never engage? did one inject dominate the clock?), and who else should be in the room next time (legal? comms? a specific vendor on-call?). Concrete, not generic. -->

- {{specific scenario or capability to test next, and why — usually because a gap from §6 needs a follow-up exercise to validate the fix}}
- {{format adjustment — duration, role coverage, materials, facilitation style}}
- {{participants to add or rotate in, with rationale}}
- {{...}}

## 9. Appendices

### A. Decision log (raw)

<!-- drafter: embed the full content of forms/decision-log.md here verbatim, preserving timestamps and authorship. -->

{{embedded decision log}}

### B. Gaps captured during exercise

<!-- drafter: embed the full content of forms/gaps-and-findings.md here verbatim. The categorized version is in §6 above; this is the raw capture for traceability. -->

{{embedded gaps and findings}}

### C. Attendance

<!-- drafter: embed the full content of forms/attendance.md. Anonymize names to roles only if --audience is regulator or board. -->

{{embedded attendance}}

### D. Timeline (raw)

<!-- drafter: embed the full content of forms/timeline-reconstruction.md. The synthesized version is in §3 above; this is the raw capture. -->

{{embedded timeline}}

---

> *AAR drafted by `/tabletop-aar` from filled forms in `{{exercise path}}`. Findings cite the decision log; corrections welcome — open the markdown and edit, then re-export HTML if used.*
