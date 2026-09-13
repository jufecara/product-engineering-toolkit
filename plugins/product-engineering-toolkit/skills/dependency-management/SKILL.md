---
name: dependency-management
description: "Dependency and environment management practices for any project: version pinning, lockfile discipline, and automated update workflows. Use when setting up a new project's dependency hygiene, or reviewing an existing project for version drift and unmanaged updates."
---

# Dependency Management

> Stack-agnostic — applies to npm/yarn/pnpm, pip/poetry, cargo, bundler, go modules, etc.

## 1. Pin the runtime

- Commit a runtime version file the ecosystem's tools respect (`.nvmrc`, `.tool-versions`,
  `runtime.txt`, `rust-toolchain.toml`, etc.).
- Declare a minimum supported version in the manifest (`engines` in `package.json`, `python_requires`
  in `pyproject.toml`, etc.) so an incompatible environment fails fast with a clear message
  instead of a confusing runtime error later.

## 2. Lockfile discipline

- Always commit the lockfile. It is the actual source of truth for what gets installed —
  the manifest alone only specifies ranges/intents.
- Use the package manager's frozen/CI install mode (`npm ci`, `poetry install --no-update`,
  `bundle install --frozen`) in CI and Docker builds — never a command that can silently rewrite
  the lockfile mid-pipeline.
- Verify lockfile-manifest sync explicitly in CI: run a clean install, then check `git diff` on
  the lockfile is empty. This catches a manifest edit that wasn't followed by an install.

## 3. Version pinning philosophy

- Prefer exact versions over floating ranges (`save-exact`/equivalent) for reproducibility across
  machines and over time — a "^1.2.3" range means different installs on different days resolve
  to different actual code.
- When a transitive dependency has a known vulnerability that the direct dependency hasn't
  patched yet, use the package manager's override/resolution mechanism as a narrow, temporary,
  documented fix — not as a default way of managing versions.

## 4. Automated updates

- Configure an update bot (Dependabot, Renovate, or equivalent) on a defined schedule (weekly is
  a reasonable default) targeting the integration branch, not the release branch directly.
- Label bot PRs distinctly and use a scoped commit-message prefix so they're easy to filter in
  history.
- Cap the number of open bot PRs at once so review capacity isn't overwhelmed.
- Route bot PRs through the same CI gate as human PRs — never merge an update without lint,
  test, and audit passing.

## 5. Before adding any new dependency

- Check its maintenance status (recent releases, open critical issues, download/adoption trend).
- Check its security posture (known advisories, transitive dependency count/depth).
- Prefer a smaller, well-scoped library over a large framework-like dependency for a narrow need.

## Verification checklist

- [ ] Runtime version pinned in a file the tooling reads, and declared as a manifest minimum.
- [ ] Lockfile committed; CI uses a frozen install and checks lockfile/manifest sync.
- [ ] Exact versions preferred; any override/resolution is narrow and documented.
- [ ] Automated dependency updates configured with schedule, labels, and a PR cap.
- [ ] Bot PRs go through the same CI gate as any other PR.
