# Security Policy

## Reporting a vulnerability

If you discover a security vulnerability in `claude-tabletop`, please **do not open a public issue**. Instead, use GitHub's private vulnerability reporting:

> [Report a vulnerability](https://github.com/cjcsecurity/claude-tabletop/security/advisories/new)

This routes the report directly to the maintainers with no public disclosure. We aim to acknowledge within **72 hours** and triage within **7 days**.

## Scope

This project ships two Claude Code skills (Markdown, JSON-shaped reference data, and one self-contained HTML template). It does **not** ship runtime code that processes untrusted input or makes network calls. The most likely vulnerability classes here are:

- **Prompt-injection vectors in scenario or template content** that could mislead a Claude session running the skill
- **HTML/JS issues in the runbook template** (`skills/tabletop-exercise/assets/runbook-template.html`) such as XSS via injected scenario content, broken CSP-relevant patterns, or `localStorage` data leakage between scenarios
- **Compliance / framework mapping inaccuracies** that could lead a user to false-positive audit evidence (treat these as security-relevant even though they're not classic vulnerabilities)

Out of scope:

- Bugs in user-generated runbooks (the skill produces these; once they live in your repo, they're yours)
- Issues in third-party `awesome-list` entries that point at this project
- Theoretical issues without a concrete reproduction scenario

## Disclosure

We follow coordinated disclosure. Once a fix is merged, a security advisory will be published in this repository's [Security Advisories](https://github.com/cjcsecurity/claude-tabletop/security/advisories) tab with credit to the reporter (unless anonymity is requested).

## Supported versions

Only the latest minor version on `main` is supported. Pin to a release tag (`v0.1.0`, etc.) for reproducible installs.
