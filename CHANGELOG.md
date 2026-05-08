# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- `/tabletop-exercise` now prompts interactively for setup. After project recon, the skill asks one round of questions (duration, audience/departments, difficulty, headcount) via a single `AskUserQuestion` call before scenario triage. Replaces the previous flag-only interface.
- All previous flags (`--duration`, `--audience`, `--difficulty`, `--scenario`, `--frameworks`, `--no-html`, `--campaign`, `--domain`) are retained as a power-user fast path: passing a flag skips the matching interactive prompt, so scripted invocations stay flagless-equivalent.

### Added

- New `--headcount <range>` flag (`2-4` / `5-8` / `9-15` / `16+`) and matching interactive prompt. The headcount value drives role-table row count, pre-populates `forms/attendance.md` with the right number of slots, and adds a breakout-group recommendation in `facilitator-notes.md` for `9-15` and `16+`.
- The audience / departments selection now also influences which roles appear in the role table (e.g., `cross-functional` adds Comms Lead and Legal/Privacy) and biases NPC selection from `references/persona-bank.md`.

## [0.1.0] — 2026-05-07

Initial public release.

### Added

- `/tabletop-exercise` skill — generates a complete tabletop exercise package tailored to the project in the current working directory.
  - Project recon scans README, manifests (Python, Node, Go, Rust, Ruby, JVM), IaC (Terraform, K8s, Helm, Pulumi), and CI/CD configs to infer stack and risk surface.
  - Scenario library with 54 entries across 9 domains: cybersec, prodsec, devops/sre, privacy/compliance, data/ml, platform, mobile, ai-safety, business-continuity.
  - 38 inject archetypes and 28 NPC personas for vivid, branchable exercise design.
  - Single-file interactive HTML runbook with live exercise timer, per-inject reveal overlays, decision-log auto-timestamping, localStorage form persistence, dark/light themes, print stylesheet, and JSON export.
  - Markdown artifacts: facilitator runbook, participant packet, standalone inject deck, facilitator-prep notes, and 5 fillable forms.
  - Optional `--frameworks` flag with control-ID tagging across NIST CSF 2.0, SOC 2, PCI DSS v4, ISO 27001:2022, HIPAA, GDPR, and MITRE ATT&CK; auto-emitted coverage matrix at runbook end.
- `/tabletop-aar` skill — drafts the After-Action Report from filled forms or the HTML runbook's JSON export.
  - Audience-tuned register: `internal`, `leadership`, `regulator`, `board`.
  - Severity rubric (P0/P1/P2) with concrete material-harm criteria.
  - Blameless framing enforced via template; specificity enforced via evidence-citation requirements.
  - Auto-maintained `INDEX.md` per project listing all completed exercises.

### Notes

- Both skills install to `~/.claude/skills/`. See `docs/INSTALL.md`.
- A "Performance contract" section in `tabletop-exercise/SKILL.md` constrains generation to a 5-10 minute wall-clock target by mandating a copy-then-edit pattern for the HTML output (vs. one-shot full-file rewrite).
