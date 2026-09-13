---
name: repo-hygiene
description: "Repository and contributor-experience hygiene for any project: standard root docs, issue/PR templates, branching policy, and agent-facing project documentation (CLAUDE.md/AGENTS.md). Use when bootstrapping a new repo's contributor experience, or reviewing an existing repo that's missing standard docs or has undocumented conventions."
---

# Repository Hygiene

> Stack-agnostic — applies to any git repository regardless of language or deployment target.

## 1. Standard root documentation

- `README.md`: what the project is, why it exists, how to run it locally (the exact commands),
  and where to find deeper docs.
- `CONTRIBUTING.md`: workflow expectations — branch naming, commit conventions, how to run the
  validation pipeline locally before opening a PR, how reviews work.
- `CODE_OF_CONDUCT.md` if the project accepts outside contributions.
- `SECURITY.md`: a private vulnerability-reporting channel (email or platform's private
  advisory feature) — never ask reporters to open a public issue for a vulnerability.
- `LICENSE`.

## 2. Issue and PR templates

- `.github/ISSUE_TEMPLATE/` (or equivalent for the hosting platform) with at least a bug-report
  and a feature-request template, so reports arrive with the information needed to act on them.
- A pull-request template that prompts for: what changed, why, how it was tested, and any
  follow-up needed — keeps review consistent even as contributors change.

## 3. Branching policy, stated explicitly

- Name the release branch and the integration branch explicitly (e.g. `main` = release,
  `dev`/`develop` = integration) and state where feature branches fork from and merge into
  (e.g. `feat/<name>` branches off the integration branch).
- State plainly: "do not merge without a green build" — make the CI-gate expectation explicit
  rather than assumed.

## 4. Explicit "do not touch" boundaries

- Where a directory or config is intentionally minimal, generated, or exported from another tool
  (icon assets, generated API clients, vendored code, a deliberately minimal build-plugin config),
  say so explicitly in the project's docs. This prevents a well-intentioned refactor (human or
  AI agent) from "cleaning up" something that's correct as-is.

## 5. Single-sourced values

- Don't duplicate a value (version string, config constant, feature flag list) across multiple
  files by hand. Read it once from its source of truth (e.g. inject the manifest's version into
  a build-time constant) so it can't drift out of sync.

## 6. Agent-facing project documentation

Maintain a project-root file the coding agent reads first (commonly `CLAUDE.md` or `AGENTS.md`)
covering:

- Essential commands as a copy-pasteable block (install, dev, build, lint, format, typecheck,
  test) — an agent (and a new human contributor) should never have to guess these.
- An architecture map: where state lives, where UI/interface logic lives, and any data-shape
  invariants that matter (e.g. "this array's index encodes row/col — document any change to
  this layout").
- Framework/language-specific gotchas stated as explicit rules, especially ones that are easy
  to get subtly wrong (state-management footguns, concurrency rules, a required error-handling
  pattern).
- A pointer to the security policy doc and a restatement of the required validation commands
  (lint, format, typecheck, test, dependency audit).
- The expected local workflow order: implement → lint → typecheck → build/test → manual check,
  every time, not "run whatever seems relevant."

## Verification checklist

- [ ] README, CONTRIBUTING, SECURITY, LICENSE all present and current.
- [ ] Issue and PR templates exist.
- [ ] Branching policy stated explicitly somewhere a new contributor will find it.
- [ ] Any intentionally-untouched directory/config says so explicitly.
- [ ] No hand-duplicated version/constant values across files.
- [ ] CLAUDE.md/AGENTS.md exists with commands, architecture invariants, and a security-policy
      pointer.
