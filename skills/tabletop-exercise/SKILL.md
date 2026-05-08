---
name: tabletop-exercise
description: Generate a polished, engaging tabletop exercise (TTX) runbook for the current project — covering cybersecurity, product security, DevOps/SRE, privacy/compliance, data/ML, or any other technical domain. Surveys the project to pick scenarios that match the actual stack and risk surface, then produces a facilitator runbook, participant packet, timed injects, fillable forms, and an interactive HTML version with a live exercise timer. Use when the user asks to "create a tabletop exercise", "generate a TTX", "build an incident drill", "make an IR exercise", "draft a war-game scenario", or similar. Pairs with `/tabletop-aar` for After-Action Report drafting.
---

# /tabletop — generate a tabletop exercise runbook

You produce a complete tabletop exercise (TTX) package tailored to the project in the current working directory. Output is a folder of artifacts the user can run a real exercise from, plus an interactive HTML version for live facilitation.

## Inputs

The skill is interactive: after a fast project recon (Step 1) it asks one round of setup questions (Step 1.5), then runs scenario triage (Step 2). Every input also accepts a flag, and **passing a flag skips the matching prompt** — so the same skill works flagless for first-timers and fully-flagged for scripted / repeat use. If all interactive inputs are supplied as flags, Step 1.5 is skipped entirely.

### Asked interactively (with flag fast-paths)

| Input | Flag | Values | Default |
|-------|------|--------|---------|
| Duration | `--duration <len>` | `30m`, `60m`, `90m`, `half-day`, `full-day` | `90m` |
| Audience / departments | `--audience <who>` | `eng`, `eng+leadership`, `cross-functional`, `board` | `eng+leadership` |
| Difficulty | `--difficulty <lvl>` | `basic`, `intermediate`, `advanced` | `intermediate` |
| Headcount | `--headcount <range>` | `2-4`, `5-8`, `9-15`, `16+` | `5-8` |
| Scenario (Step 2 triage) | `--scenario <slug>` | any slug from `references/scenario-library.md` | (triage picks from 3) |

### Flag-only (not surfaced interactively)

| Flag | Values | Default | Why flag-only |
|------|--------|---------|---------------|
| `--domain <name>` | `cybersec`, `prodsec`, `devops`, `privacy`, `data-ml`, `platform`, `mobile`, `ai-safety` | (inferred from recon) | Recon usually picks the right domain; manual override is rare. |
| `--frameworks <list>` | comma-sep: `NIST-CSF`, `SOC2`, `PCI`, `ISO27001`, `HIPAA`, `GDPR`, `MITRE-ATTACK` | (off) | Most exercises don't tag controls; opt-in keeps the prompt round focused. |
| `--no-html` | (presence) | (HTML on) | Default-on; opting out is rare. Useful for smoke tests. |
| `--campaign <name>` | string | none | Multi-session linked exercises — advanced / niche. |

## Performance contract

A full run should finish in **5-10 minutes wall-clock**, not 30+. If you're approaching 15 minutes without writing any output files, you are off-contract. Common causes and fixes:

- **Loading every reference file into context upfront** → don't. `references/scenario-library.md` is 80KB; only Read the section you need. `references/inject-patterns.md` is 45KB; same. Pull excerpts, not whole files.
- **Trying to write `RUNBOOK.html` as one giant Write call** → don't. Use the copy-then-edit pattern in Step 5. This is the #1 stuck-run cause.
- **Generating `RUNBOOK.md` as one ~1000-line Write** → split if it exceeds ~500 lines. Use Write for an initial skeleton, then Edit the placeholder sections. (The markdown is more forgiving than the HTML — one Write up to ~500 lines is fine.)
- **Re-reading the same reference file multiple times** → Read once per section, hold context.
- **Re-deriving the scenario from scratch after the user picks** → the user's pick + your earlier triage are sufficient; don't re-evaluate.

If you notice yourself spending more than ~3 minutes on any one step without producing a file, STOP, write what you have, and continue.

## Workflow

### Step 1 — Project recon (silent, fast)

Read in parallel:

- `README.md`, `README.txt`, `README.rst` (any of)
- Manifest files: `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `Gemfile`, `pom.xml`, `build.gradle`, `composer.json`, `mix.exs`
- IaC and deploy: `Dockerfile`, `docker-compose*.yml`, `kubernetes/`, `k8s/`, `terraform/`, `*.tf`, `helm/`, `pulumi/`, `ansible/`, `serverless.yml`, `.github/workflows/`, `.gitlab-ci.yml`, `Jenkinsfile`, `cloudbuild.yaml`
- Security and config hints: `.env.example`, `auth/`, `security/`, `SECURITY.md`, `.well-known/security.txt`
- Repo-local `CLAUDE.md` if present (extra context the user has curated)

Infer: language stack, deployment model (cloud provider, container/serverless/bare-metal), data sensitivity hints (PII keywords, payment libs, healthcare libs, auth providers), external integrations, CI/CD model. Do NOT spend more than ~10 file reads on this — speed matters; the exercise itself doesn't need encyclopedic recon.

If the project is essentially empty (no README, no manifests), tell the user you can't tailor a scenario without more context and ask them what the project does.

### Step 1.5 — Interactive setup

Ask the setup questions in **one `AskUserQuestion` call** so the user fills out everything in a single screen. **Skip any question whose corresponding flag was already passed** (`--duration`, `--audience`, `--difficulty`, `--headcount`). If all four were passed, skip Step 1.5 entirely and proceed to scenario triage. If only some were passed, ask the remaining ones in a single call.

Resolve each unflagged input via these question shapes:

1. **Duration** — options: `60m — focused`, `90m — standard (recommended)`, `Half-day (3-4h) — deep dive`, `Full-day workshop`. (`AskUserQuestion` caps at 4 options; `30m` is intentionally not in the list. `AskUserQuestion` always exposes an "Other" free-text field — if the user types `30m` there, accept it. They can also re-invoke with `--duration 30m` for a flagless 30-min smoke test.)
2. **Who's playing?** — options: `Engineering only`, `Eng + Security + Leadership (recommended)`, `Cross-functional — eng + sec + legal + comms + execs`, `Board / executive briefing`. Map the chosen label back to `eng` / `eng+leadership` / `cross-functional` / `board` for downstream use.
3. **Difficulty** — options: `Basic — newer team, walk-through tone`, `Intermediate — practiced team (recommended)`, `Advanced — high ambiguity, heavy branching`.
4. **Headcount** — options: `2-4 people — small group, lots of discussion`, `5-8 people — standard size (recommended)`, `9-15 people — larger room, breakouts useful`, `16+ — workshop format, breakout groups required`.

After the user answers, give a one-line confirmation of **all four resolved values** — flag-supplied and interactive-answered alike, in a consistent order (duration · audience · difficulty · headcount). Example: "Got it — 90m, cross-functional, intermediate, 5-8 people. Let me line up three scenarios that fit." Then continue to Step 2. Don't re-ask or second-guess.

**When Step 1.5 is skipped entirely** (all four flags passed): still emit the same one-line confirmation of the four resolved values before moving on. This is the user's only signal that the skill registered their flags correctly.

**How these inputs flow into later steps** (referenced again where they apply):

- **Duration** → phase count and inject density (see `references/runbook-template.md`).
- **Audience / departments** → register, NPC selection, and which roles appear in the role table (e.g., `cross-functional` adds Comms Lead and Legal/Privacy; `board` strips operational detail and skips the scoring rubric).
- **Difficulty** → branching depth, ambiguity, wild-card frequency.
- **Headcount** → number of role-table rows, number of slots pre-populated in `forms/attendance.md`, and a recommendation in `facilitator-notes.md` for breakout groups when `9-15` or `16+`.

### Step 2 — Scenario triage

Read `references/scenario-library.md` for the catalog.

If `--scenario` was given, skip to Step 3.

Otherwise, pick the **3 most relevant scenarios** for what you saw in Step 1, weighted by:
1. Direct stack relevance (a Postgres-using web app gets DB-corruption higher than a CLI library does)
2. Realistic risk for this kind of product (a payment app gets PCI-relevant scenarios; a privacy-data product gets GDPR scenarios)
3. Diversity of domain (don't propose 3 cybersec scenarios — mix in DevOps and one wild-card)

Present them via `AskUserQuestion` with crisp one-line descriptions of each. Include a fourth "Other / let me describe" path so the user can request something custom. After they choose, briefly confirm the scenario and move on.

### Step 3 — Build the runbook

Use `references/runbook-template.md` as the master Markdown structure. Use `references/inject-patterns.md` to flesh out timed injects. Use `references/persona-bank.md` to give NPCs personality. Use `references/framework-controls.md` only when frameworks were selected (via `--frameworks`).

Apply the Step 1.5 inputs as you build:
- **Roles table**: scale row count to the headcount band (2-4 → 3 roles + facilitator; 5-8 → 4-5 roles; 9-15 → 5-6 roles; 16+ → 6 roles plus a note recommending two breakout groups). Choose role *types* from the audience selection (e.g., add Legal/Privacy and Comms Lead for `cross-functional`).
- **NPCs**: weight `references/persona-bank.md` picks toward the departments in the room — a `board` audience meets the panicked CEO and PR lead more than the on-call SRE.
- **Phase + inject counts**: per duration band in `references/runbook-template.md`.

Tone: write the runbook like a tabletop RPG module. Boxed read-aloud text. Vivid scenario openers. NPCs with voice. Time pressure. Branching consequences. Avoid corporate-compliance dryness — this should be something facilitators are excited to run.

### Step 4 — Write artifacts

Create directory: `tabletop-exercises/<YYYY-MM-DD>-<scenario-slug>/`

Write these files (all in that directory):

| File | Purpose |
|------|---------|
| `RUNBOOK.md` | Full facilitator guide. Has all spoilers, branches, scoring criteria. |
| `PARTICIPANT-PACKET.md` | Pre-read for participants. Scenario context only — NO injects, NO branches, NO answers. |
| `INJECTS.md` | Timed inject deck pulled out as a standalone for fast facilitator reference during the exercise. |
| `facilitator-notes.md` | Pre-exercise prep checklist: room setup, materials, pre-briefs, role assignments. |
| `forms/attendance.md` | Who's playing what role. Pre-populate the row count based on headcount (e.g., 8 empty rows for `5-8`, 15 for `9-15`) so the facilitator just fills in names. |
| `forms/decision-log.md` | Timestamped decision capture during the exercise. |
| `forms/timeline-reconstruction.md` | What happened when, filled out during/after. |
| `forms/gaps-and-findings.md` | Issues surfaced during the exercise. |
| `forms/aar-template.md` | Empty After-Action Report skeleton for the AAR companion to ingest. |

### Step 5 — Generate the HTML (FAST PATH — read this carefully)

Unless `--no-html` was passed, also produce `RUNBOOK.html` in the same directory.

**DO NOT regenerate the entire HTML file with one Write call.** The template is ~1300 lines / 44KB. Rewriting it whole is the #1 cause of slow/stuck runs in this skill. Use the **copy-then-edit** pattern instead:

1. **Copy the template** to the output location with one Bash call:
   ```
   cp ~/.claude/skills/tabletop-exercise/assets/runbook-template.html tabletop-exercises/<slug>/RUNBOOK.html
   ```
2. **Replace the two single-token data attributes** (one Edit call each):
   - Edit `<!-- TTX:DURATION_SECONDS -->` → the duration in seconds (e.g. `5400` for 90m)
   - Edit `<!-- TTX:SCENARIO_SLUG -->` → the kebab-case scenario slug
3. **Replace each placeholder block with a separate Edit call.** Each block is bounded by `<!-- TTX:SECTION_START -->` and `<!-- TTX:SECTION_END -->` markers. Replace the entire block (markers included, OR keep markers as comments — your call). Do this for:
   - `TTX:META_START` … `TTX:META_END` — title `<h1>` + subtitle line
   - `TTX:SCENARIO_SUMMARY_START` … `TTX:SCENARIO_SUMMARY_END` — 2-3 paragraph summary
   - `TTX:ROLES_START` … `TTX:ROLES_END` — roles table rows
   - `TTX:PHASES_START` … `TTX:PHASES_END` — sequence of phase blocks (the template includes one fully-built example phase showing all callout types — clone its structure for each phase you generate)
   - `TTX:DECISION_LOG_START` … `TTX:DECISION_LOG_END` — initial empty decision log table
   - `TTX:HOTWASH_START` … `TTX:HOTWASH_END` — hotwash questions with `<textarea>` answer fields
   - `TTX:AAR_PROMPTS_START` … `TTX:AAR_PROMPTS_END` — post-exercise reflection fields

This pattern is **6-8 small Edits + 1 cp** instead of one giant Write. Each Edit is a few hundred tokens at most. The whole HTML phase finishes in 1-3 minutes vs 15-30+ for the rewrite-whole approach.

**Do not strip or modify** the embedded `<style>` or `<script>` blocks. They power the timer, persistence, reveal overlays, and JSON export. If you find yourself rewriting CSS or JS, stop — you're doing it wrong.

**Do not read the template into context just to copy it** — the `cp` command does that for you without burning tokens. You only need to read sections of the template to understand what each placeholder should look like, and only do that for placeholders you're unsure about.

### Step 6 — Output summary

Tell the user concisely what was created and the suggested next steps:

```
✓ Created tabletop-exercises/2026-05-07-<slug>/

  Markdown:
    - RUNBOOK.md (facilitator — full spoilers)
    - PARTICIPANT-PACKET.md (pre-read for players)
    - INJECTS.md (live deck)
    - forms/ (5 fillable forms)
    - facilitator-notes.md (your prep checklist)

  Interactive:
    - RUNBOOK.html (open in browser to facilitate live)

  Next:
    1. Send PARTICIPANT-PACKET.md to attendees ahead of time
    2. Open RUNBOOK.html in a browser to run the exercise
    3. After: /tabletop-aar to draft the After-Action Report
```

Do not dump the runbook content into the chat — just the summary. The artifacts are the deliverable.

## Quality bar

The runbook should pass these tests:

- **Vividness**: a facilitator can read the boxed scenario opener aloud and the room feels the tension
- **Specificity**: injects reference *this* product's actual stack, not generic "your application"
- **Decisions, not lectures**: each phase forces a real choice with consequences, not a multiple-choice quiz
- **Roles have teeth**: every named role has at least one moment where they own a decision
- **Branches matter**: at least 2 inject branches change the trajectory of later phases
- **Closes the loop**: the hotwash and AAR template surface gaps that turn into action items, not vague feel-good summaries

If a generated runbook fails any of these, fix it before declaring done.

## Edge cases

- **Project is mostly docs / empty repo**: ask the user what the product does in 1-2 sentences, then proceed
- **Project is enormous monorepo**: pick the top-level directory the user most recently worked in (check `git log -10 --name-only`); if unclear, ask
- **User wants a domain you can't connect to the stack**: just generate it. The skill should not refuse a request because the stack doesn't perfectly match — note the mismatch briefly and proceed.
- **Output dir already exists**: append a `-2`, `-3` suffix to the date-slug. Do not overwrite prior exercises.
- **`--campaign` flag**: write to `tabletop-exercises/<campaign-name>/<NN>-<slug>/` and reference prior session AARs if they exist in the campaign dir.

## Reference files in this skill

- `references/scenario-library.md` — catalog of ~40 scenarios across all domains, with stack-relevance hints
- `references/inject-patterns.md` — reusable inject archetypes by phase and type
- `references/persona-bank.md` — NPC personalities (panicked CEO, press-friendly comms, unreachable contractor, etc.)
- `references/framework-controls.md` — control ID lookups for each compliance framework (used only when `--frameworks` was passed)
- `references/runbook-template.md` — master Markdown structure
- `assets/runbook-template.html` — interactive HTML template

Read these on demand — don't pre-load everything. Read scenario-library and inject-patterns early; read framework-controls only when frameworks were selected; read persona-bank when you're fleshing out NPCs.
