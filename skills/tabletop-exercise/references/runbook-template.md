# Runbook template

This file defines the master Markdown shape the `/tabletop` generator follows when writing `RUNBOOK.md` in the user's project. Everything below the "Template begins" line is the literal scaffold; the generator substitutes scenario-specific content into the `{{double-brace}}` placeholders and follows the `<!-- inline notes -->` to decide which sections to keep, expand, or omit.

## How the generator uses this file

- **Substitute every `{{placeholder}}`** with concrete scenario content. Never leave a literal `{{...}}` in the output. Never invent placeholders not in this template.
- **Phase count scales with `--duration`**. 30m: 2 phases. 60m: 3 phases. 90m (default): 4 phases. half-day: 5-6 phases. full-day: 6-8 phases. Phases are 15-25 minutes each — never less than 12, never more than 30.
- **Total inject count scales with duration**. 30m: 4-6. 60m: 6-9. 90m: 8-12. half-day: 18-25. full-day: 30-45. Each phase contains 3-5 injects, never more than 7. **Counting rule**: alternative-branch injects (e.g. 1.2A / 1.2B / 1.2C) count as ONE slot, not multiple — only one branch fires per run. Count distinct *trigger points*, not the variants under each.
- **Every inject must have either a branch or a decision tied to it** — no purely informational injects. If something is "just context," roll it into the phase opener instead.
- **At least 2 of the inject branches must change the trajectory of later phases** — not just cosmetic differences. A branch that only changes a single follow-up message is too shallow.
- **Coverage matrix is conditional**. Include the `## Coverage matrix` section only if `--frameworks` was passed. Otherwise omit the entire section, including the heading.
- **Scoring rubric is optional but default-on**. Include it unless the audience is `board` (skip — boards don't score themselves) or duration is `30m` (skip — too short to score meaningfully).
- **Roles table** must include facilitator + evaluator (optional row) + 3-6 scenario-specific roles. Scenario-specific roles come from the scenario itself; pull names from `references/persona-bank.md` only as flavor for NPCs, not for participant roles.
- **Hotwash always has 10 questions**. Seven specific to the scenario, three generic-but-tailored ("what surprised you", "what would you change about our process", "where did time pressure cost us").
- **Tone rules**: vivid in read-aloud blocks (sensory detail, specific timestamps, named systems from the actual stack), neutral-direct in instructions to the facilitator, never corporate-passive ("it was decided that"), never gimmicky ("buckle up, team!"). Read-aloud blocks should sound like the cold open of a tech thriller, not a security awareness video.
- **Specificity over generality**. If the recon turned up "Postgres on RDS, Datadog, GitHub Actions, Auth0" — name those exact systems in the injects. "Your application's database" is a failed inject. "The `users` table in `prod-rds-2` just got a row count drop on Datadog dashboard `db-health`" is a passing inject.
- **Time-on-clock format** is `T+0`, `T+12`, `T+45m`, etc. — relative to exercise start, not wall clock. Write durations as `T+0 to T+22` for phase ranges.
- **Phase names** should be active and specific to the scenario, not generic. Bad: "Initial Response." Good: "First sirens — the Datadog page that started it." Generator should generate phase names from the scenario beats, not template defaults.

---

## Template begins

```markdown
# {{Scenario Title}}

> **Domain**: {{domain}} · **Duration**: {{duration}} · **Audience**: {{audience}} · **Difficulty**: {{difficulty}}
> Generated {{YYYY-MM-DD}} for {{project-name-from-recon}}

<!-- Generator: project-name comes from package.json#name, pyproject.toml [project] name, the repo root directory name, or the README's H1 — in that priority order. -->

## Quick reference

| # | Phase | T-window | Key decision | Tested capability |
|---|-------|----------|--------------|-------------------|
| 1 | {{phase 1 name}} | T+0 → T+{{n}} | {{the call that has to be made}} | {{e.g. detection time}} |
| 2 | {{phase 2 name}} | T+{{n}} → T+{{m}} | {{...}} | {{...}} |
| 3 | {{phase 3 name}} | T+{{m}} → T+{{p}} | {{...}} | {{...}} |
| 4 | {{phase 4 name}} | T+{{p}} → T+{{end}} | {{...}} | {{...}} |

<!-- Generator: one row per phase. Key decision is the single most consequential call in that phase. Tested capability is one phrase, not a sentence. -->

## Legend

- 📢 Read-aloud — facilitator says verbatim. Don't paraphrase or skip; the wording is doing work.
- 💉 Inject — revealed at the marked time. Hidden from participants beforehand. The HTML runbook collapses these by default.
- ⚡ Decision point — team must choose. Document the choice in `forms/decision-log.md`.
- 🌿 Branch — different next-injects depending on the choice. Facilitator picks the matching branch and continues.
- 👤 NPC voice — facilitator (or designated player) plays a role. Voice cues in italics under the line.
- 🎯 Capability tested — what this inject or decision is probing for in the scoring rubric.

## Scenario summary

{{2-3 paragraphs setting the world. First paragraph: the product and team as it normally is — make it feel like a Tuesday. Second paragraph: what just happened (the precipitating event), in enough detail that participants understand the stakes but not so much that the rest of the runbook is spoiled. Optional third paragraph: who else is in the building — the customers, regulators, press, vendors who will plausibly enter the story.}}

<!-- Generator: this is what goes into PARTICIPANT-PACKET.md too. Keep it spoiler-free past the precipitating event. Do NOT preview later injects here. Length: 250-450 words. -->

## Roles & responsibilities

| Role | Played by | Owns |
|------|-----------|------|
| Facilitator | _________ | Pacing, injects, timekeeping, calling branches |
| Evaluator (optional) | _________ | Notes, scoring against the rubric, hotwash prompts |
| {{role 1}} | _________ | {{what they own in this scenario, in 8-12 words}} |
| {{role 2}} | _________ | {{...}} |
| {{role 3}} | _________ | {{...}} |
| {{role 4}} | _________ | {{...}} |
| {{role 5}} | _________ | {{...}} |

<!-- Generator: 3-6 scenario-specific roles in addition to facilitator/evaluator. Common roles by domain:
  cybersec: Incident Commander, On-call SRE, Security Lead, Comms Lead, Legal/Privacy, Exec Sponsor
  devops: Incident Commander, On-call SRE, Platform Lead, Customer Support Lead, Comms Lead
  privacy: DPO, Legal, Comms, Security Lead, Customer Support Lead
  prodsec: Incident Commander, AppSec Lead, Eng Lead, Comms, Legal
Pick the right set; do NOT include all of them. Every named role MUST own at least one decision somewhere in the runbook. -->

## Pre-exercise setup (T-pre)

- [ ] Send `PARTICIPANT-PACKET.md` to attendees ≥ 24 hours before
- [ ] Confirm role assignments (use `forms/attendance.md`)
- [ ] Print or pull up `forms/decision-log.md` and `forms/timeline-reconstruction.md`
- [ ] Open `RUNBOOK.html` in a browser if facilitating live (the in-runbook timer makes pacing easier)
- [ ] Read through INJECTS.md once end-to-end so you can see the branches before you have to call them
- [ ] {{any scenario-specific prep — e.g. "Stage a fake Datadog dashboard screenshot in case the team asks for one"}}

## Phase 1 — {{phase 1 name}} (T+0 to T+{{phase 1 end}})

### 📢 Read-aloud opener

> {{4-6 lines of vivid scene-setting that the facilitator reads verbatim. Specific time of day, specific named systems, sensory detail, ending on the precipitating event. The room should feel the tension after the last sentence. Example shape: "It's 14:47 on a Wednesday. The deploy bot in #releases just announced that v2.41.3 went green to prod thirteen minutes ago. Sarah is half-watching the Datadog dashboard out of habit while she finishes a sandwich. Then the auth-service p99 latency graph goes from a flat 80ms to a 4-second wall in under a minute. Her phone buzzes. PagerDuty: SEV2, AuthServiceDown."}}

### 🎯 Capabilities tested in this phase
- {{capability 1 — e.g. "Detection: how fast does the team move from page to declared incident"}}
- {{capability 2 — e.g. "Triage: separating signal from noise"}}
- {{capability 3}}

### 💉 Inject 1.1 — {{inject name}} (T+{{time}})

{{The inject content. 1-3 sentences, written as if it's arriving in the channel/system the participants would actually see it in. Include sender, channel, format. Make it feel like a real message, not a summary of one.}}

**🌿 Branch on team's response within {{N}} minutes:**
- If team {{action X — e.g. "declares an incident and pages the IC"}} → proceed to **Inject 1.2A**
- If team {{action Y — e.g. "investigates without declaring"}} → proceed to **Inject 1.2B**
- If team takes no action in {{N}} minutes → drop **Inject 1.2C** (wild-card escalator)

### 💉 Inject 1.2A — {{name}} (T+{{time}})
{{...}}

### 💉 Inject 1.2B — {{name}} (T+{{time}})
{{...}}

### 💉 Inject 1.2C — {{name}} (T+{{time}})
{{...}}

### ⚡ Decision point 1 — {{decision name}}

**The choice**: {{forced choice in 1-2 sentences. Frame it as a real trade-off where both options have a real cost. Avoid one obvious right answer.}}

**Owns this call**: {{role from the roles table}}

**Document in decision log**: who made the call, at what T+time, what the rationale was, who was in the loop.

<!-- Generator: 3-5 injects per phase, never more than 7. At least one inject per phase MUST have a real branch (not "tell me about it" branches — actual divergent next-injects). Decision points happen 1-2 times per phase. The decision in phase 1 is usually about declaration/severity; in phase 2 about containment; in phase 3 about external comms; in phase 4 about all-clear. -->

## Phase 2 — {{phase 2 name — typically Escalation}} (T+{{phase 2 start}} to T+{{phase 2 end}})

### 📢 Read-aloud bridge

> {{2-4 lines of read-aloud that connects phase 1's resolution into phase 2's pressure. Time has passed. Stakes have widened. New characters arrive. Don't recap — escalate.}}

### 🎯 Capabilities tested in this phase
- {{capability — typically: scope expansion handling, cross-team coordination, external escalation}}

### 💉 Inject 2.1 — {{name}} (T+{{time}})
{{...}}

### 💉 Inject 2.2 — {{name}} (T+{{time}})
{{...}}

### 👤 NPC voice — {{NPC name and role}}

> {{Short line the NPC says, in their voice. Italicize a parenthetical voice cue beneath, e.g. "*delivered fast, slightly clipped, not waiting for response*"}}

**Where this NPC pushes**: {{what pressure they create — e.g. "wants a status page update RIGHT NOW even though the team doesn't have facts yet"}}

### ⚡ Decision point 2
{{...}}

<!-- Generator: phase 2 should introduce one NPC interaction minimum. NPCs come from references/persona-bank.md if helpful. Each NPC creates pressure on a specific axis (time, comms, legal, customer, exec) — pick the axis that's most underexercised so far. -->

## Phase 3 — {{phase 3 name — typically Decision Pressure}} (T+{{phase 3 start}} to T+{{phase 3 end}})

### 📢 Read-aloud bridge
> {{...}}

### 🎯 Capabilities tested in this phase
- {{capability — typically: external comms, legal/regulatory clock, customer-facing decisions, exec alignment}}

### 💉 Inject 3.1 — {{name}} (T+{{time}})
{{...}}

### 💉 Inject 3.2 — {{name}} (T+{{time}})
{{...}}

### 💉 Inject 3.3 — {{name}} (T+{{time}})
{{...}}

### ⚡ Decision point 3 — {{the comms call}}
{{...}}

<!-- Generator: phase 3 is the one where the team has to commit to something irreversible (or feels irreversible). Customer notification, regulator notification, public statement, taking a critical service offline. The decision should be load-bearing — phase 4 reads differently depending on the call. -->

## Phase 4 — {{phase 4 name — typically Resolution / Wind-down}} (T+{{phase 4 start}} to T+{{phase 4 end}})

### 📢 Read-aloud bridge
> {{...}}

### 🎯 Capabilities tested in this phase
- {{capability — typically: recovery decisioning, all-clear discipline, evidence preservation, handoff to longer-term remediation}}

### 💉 Inject 4.1 — {{name}} (T+{{time}})
{{...}}

### 💉 Inject 4.2 — {{name}} (T+{{time}})
{{...}}

### ⚡ Decision point 4 — {{when do we call it done}}
{{...}}

### 📢 Closing read-aloud

> {{2-3 lines that draw the curtain — not "everyone lived happily ever after," more like "the dust settles, you have a sense of what was lost, and the AAR work is now ahead of you." This sets the tone for hotwash.}}

<!-- Generator: do NOT resolve everything cleanly. Leave one or two threads dangling that the hotwash and AAR can pull on. Real incidents don't end neatly; the runbook shouldn't pretend otherwise. -->

## Hotwash (15-20 minutes after exercise ends)

Run these in order. Capture answers in `forms/gaps-and-findings.md`.

1. {{specific to scenario — e.g. "When did you actually realize this was a security incident and not just a performance problem? What was the signal that flipped it?"}}
2. {{specific to scenario}}
3. {{specific to scenario}}
4. {{specific to scenario}}
5. {{specific to scenario}}
6. {{specific to scenario}}
7. {{specific to scenario}}
8. What surprised you most about how this played out?
9. If you could change one thing about our actual response process based on this exercise, what would it be?
10. Where did time pressure cost us — a decision made too fast, or one we sat on too long?

<!-- Generator: 10 prompts always. Questions 1-7 are scenario-specific and should target the gaps the runbook was designed to surface. Questions 8-10 are stable framing prompts; keep them verbatim. -->

## Scoring rubric (optional)

<!-- Generator: include this section unless audience=board or duration=30m. -->

| Capability | Excellent (3) | Adequate (2) | Needs work (1) | Not exercised (0) |
|------------|---------------|--------------|----------------|-------------------|
| Detection time | < 5 min from inject to declared awareness | < 15 min | > 15 min, or only after a second signal | n/a — never detected |
| Severity calling | Right severity, justified, on first call | Right severity after one revision | Wrong severity persisted past phase 1 | n/a |
| Escalation correctness | Right person, right channel, right urgency | Right person but slow or wrong channel | Wrong channel or wrong person | n/a |
| Decision velocity | Calls made inside the time pressure window with documented rationale | Calls made but late, or made without documented rationale | Calls deferred or made by default (clock ran out) | n/a |
| External comms | Customer/regulator/press handled with clarity, no overcommitment, on-time | Handled but rough — overpromise, late, or off-message | Mishandled — wrong audience, wrong message, or blew the clock | n/a |
| Evidence preservation | Forensic-conscious moves throughout (snapshots, logs, decision log) | Evidence preserved retroactively | Evidence lost — host rebuilt, logs rotated, decisions undocumented | n/a |
| Recovery sequencing | Restored in priority order, with verification before all-clear | Restored mostly correctly, all-clear premature or late | Restoration order created secondary impact, or all-clear was wrong | n/a |
| {{scenario-specific capability}} | {{what 3 looks like}} | {{what 2 looks like}} | {{what 1 looks like}} | n/a |

<!-- Generator: 6-8 rows. The first 7 are stable; add 1-2 scenario-specific rows for capabilities the runbook deliberately tests (e.g. for ransomware: "ransom-decision discipline"; for GDPR: "72-hour clock awareness"). Keep the level descriptions concrete — what observable behavior maps to each level. -->

## Coverage matrix

<!-- Generator: include this section ONLY if --frameworks was passed. Otherwise omit the entire section, including the heading. -->

<!-- Generator: columns are the requested frameworks in the order they appeared in --frameworks. Rows are every inject ID and every decision point. Each cell is the most relevant control ID(s) from references/framework-controls.md, or "—" if the inject doesn't touch that framework. Multiple IDs separated by `, `. Do not invent IDs not present in framework-controls.md. -->

| Inject / Decision | NIST CSF | SOC 2 | PCI DSS | ISO 27001 | HIPAA | GDPR | MITRE ATT&CK |
|-------------------|----------|-------|---------|-----------|-------|------|--------------|
| Inject 1.1 | DE.AE-02 | CC7.2 | 10.4.1 | A.8.16 | §164.308(a)(1)(ii)(D) | — | T1190 |
| Inject 1.2A | RS.MA-01 | CC7.4 | 12.10.1 | A.5.24 | §164.308(a)(6)(i) | — | — |
| Decision 1 | RS.MA-03 | CC7.3 | 12.10.1 | A.5.25 | §164.308(a)(6)(ii) | — | — |
| {{...}} | | | | | | | |

## Appendix A — Facilitator cheatsheet

**Common stalls and how to unblock them:**
- _Team is talking but not deciding_: pause, ask "what's the next concrete action and who owns it" — do not let abstract discussion stretch past 4 minutes.
- _Team latched onto the first hypothesis_: drop a contradicting inject early, even if the schedule says later. Tunneling kills realism.
- _One person is doing all the work_: address by role, not by name — "Comms Lead, what's our status page saying right now" — to spread load.
- _Team can't find the runbook / contact list / vendor number_: that IS the finding. Note it in `forms/gaps-and-findings.md` and let the awkwardness sit.

**When to drop a wild-card inject:**
- Energy is dropping and there are 15+ minutes of phase left
- Team has converged too quickly on a tidy answer (force a complication)
- The exercise has been smooth and the audience is `eng+leadership` or higher (leadership audiences benefit from one curveball)

**How to read the room:**
- _Slow down when_: voices overlap, multiple people are taking notes that disagree, someone with authority hasn't spoken in 5+ minutes
- _Push harder when_: long silences, side conversations starting, the same point getting re-litigated
- _Hard stop when_: someone is visibly stressed in a not-productive way. Pause, name it, give a 2-minute break. The exercise is for learning, not for breaking people.

## Appendix B — Form locations

- Decision log: `forms/decision-log.md`
- Timeline reconstruction: `forms/timeline-reconstruction.md`
- Gaps and findings: `forms/gaps-and-findings.md`
- Attendance and roles: `forms/attendance.md`
- AAR template (for the post-exercise writeup): `forms/aar-template.md`

## Appendix C — Branch trace (facilitator only)

<!-- Generator: include this appendix always. It's a flat list of every branch in the runbook so the facilitator can scan during play. Format:
- Inject X.Y → if A: next is X.Z+A; if B: next is X.Z+B; if no-action in N min: next is X.Z+C
List every branch in order. Decisions don't appear here unless they fork the inject path. -->

- Inject 1.1 → if {{A}}: next is 1.2A; if {{B}}: next is 1.2B; if no action in {{N}} min: drop 1.2C
- {{...repeat for every branching inject in the runbook...}}
```

## Template ends

<!-- Anything below this line is generator notes only and does NOT appear in the output runbook. -->

### Final stylistic checklist before writing the file

Before the generator finalizes RUNBOOK.md, verify:

1. No literal `{{placeholder}}` text remains in the output.
2. Every named role in the Roles table owns at least one decision somewhere in the phases.
3. At least 2 inject branches change the trajectory of subsequent phases — not just cosmetic differences.
4. Phase durations sum to exactly the `--duration` flag value (within ±5 min of total).
5. Inject count falls within the duration band (8-12 for 90m, etc.).
6. Read-aloud blocks reference the actual stack from project recon — named systems, named services, real tooling.
7. Coverage matrix is present iff `--frameworks` was passed.
8. Scoring rubric is present iff audience ≠ board AND duration ≠ 30m.
9. Hotwash has exactly 10 numbered questions, with #8/#9/#10 being the stable framing prompts verbatim.
10. Closing read-aloud leaves at least one thread dangling — no clean fairy-tale endings.

If any of these fail, fix before writing. Don't ship a runbook that violates the structure — the HTML generator and the AAR companion both expect this shape.
