# Contributing

Thanks for considering a contribution. The project lives or dies on the quality of its scenarios, injects, and personas — those are where most PRs land.

## Most useful contributions

1. **New scenarios** in `skills/tabletop-exercise/references/scenario-library.md`. See the existing entries for the format. Each scenario needs a slug, domain tag, "best for" matching hints, duration sweet spot, difficulty range, frameworks exercised, a 4-6 line seed with real tension, key decision points, and common gaps surfaced. Avoid scenarios that already exist or that are trivial restatements.

2. **New inject archetypes or personas** in `skills/tabletop-exercise/references/inject-patterns.md` or `persona-bank.md`. Vivid > generic. Templates should read like RPG-module boxed text. Personas should have quotable voice cues.

3. **Framework controls for regimes not yet covered** — FedRAMP, CCPA, CMMC, NIS2, DORA, SOX. Use the same column shape as existing tables in `framework-controls.md`. Verify control IDs against the official source standard.

4. **Improvements to the HTML template** at `skills/tabletop-exercise/assets/runbook-template.html`. Test in headless Chromium before submitting (zero console errors, all interactivity verified working). Don't add external dependencies — this template must stay single-file and offline-capable.

5. **Sample exercise outputs** to anchor the README. A hand-curated, sanitized example exercise (markdown + HTML) makes the project way easier for new users to understand. Place under `examples/`.

## What to avoid in PRs

- Scenarios padded to "balance" the catalog — quality over count
- Generic injects ("the team gets confused") — must be specific and branchable
- Framework control IDs you're unsure are real — better to omit than fabricate
- Adding dependencies to the HTML template
- Removing the offline-capable / single-file constraint
- Emoji-driven runbook content (light Unicode glyphs only)

## PR process

1. Fork, branch, edit
2. Test your changes — at minimum, run `/tabletop-exercise --duration 30m --no-html` in a sample project and verify the markdown output is sensible. If you touched the HTML template, also verify in a browser.
3. Open a PR with a clear description of what you changed and why
4. Be ready to iterate on review

## Style conventions

- Markdown: kebab-case filenames, ATX-style headers (`## Heading`), tables for structured data
- Tone: professional but warm; not bureaucratic. Direct, specific, blameless framing in the AAR template
- Scenarios: realistic details over invented technobabble. Real CVEs, real attack patterns, real regulatory triggers

## Reporting issues

Please include:

- The skill version (commit hash) you're using
- The flags / invocation that triggered the issue
- The project type you ran it on (don't share proprietary code — a sanitized description is fine)
- Expected vs actual behavior

Thanks for helping make this better.
