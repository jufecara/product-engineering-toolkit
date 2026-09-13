---
name: security-hardening
description: "Security and supply-chain hardening practices for any codebase: dependency auditing, secrets handling, CSP/web hardening when applicable, and a security-policy document aimed at both humans and AI agents. Use when setting up a new project's security baseline, or auditing/hardening an existing project's security posture."
---

# Security Hardening

> Stack-agnostic. Apply what's relevant; skip what doesn't exist in this project (e.g. there's
> no CSP section to write if there's no browser front-end).

## 1. Supply-chain / dependency security

- Enable an audit tool for the package manager in use (`npm audit`, `pip-audit`, `cargo audit`,
  `bundler-audit`, etc.) and fail builds on high/critical findings.
- Pin exact dependency versions where the ecosystem supports it (no floating ranges) so builds
  are reproducible and a compromised "latest" can't slip in silently.
- Commit the lockfile and verify in CI that it's in sync with the manifest (fail if a clean
  install produces a diff).
- Disable arbitrary install-time script execution from dependencies when the package manager
  allows it (e.g. npm's `ignore-scripts=true`) unless a specific package legitimately needs it.
- Use version overrides/resolutions only as a targeted, documented, temporary mitigation for a
  known transitive vulnerability — not as a general practice.
- Keep automated dependency updates (Dependabot/Renovate) flowing through the audit tool rather
  than merged on trust — a bumped version still needs the same audit/lint/test gate as any other
  change before it lands.
- Review the maintenance status and security posture of any new dependency before adding it.

## 2. Secrets and environment handling

- Never commit secrets, tokens, API keys, or credentials — check `.gitignore` covers all local
  env files (`.env`, `.env.local`, etc.).
- Provide an `.env.example` with placeholder values only, as the template for local setup.
- Client-side storage (browser localStorage/IndexedDB, mobile app local storage, etc.) must never
  hold credentials, tokens, or secrets — only non-sensitive app state.
- Avoid leaking sensitive data into logs or error messages, especially in production builds.

## 3. Web app hardening (only if there's a browser-facing front-end)

- Ship a strict Content-Security-Policy: start from `default-src 'self'`, then open only what's
  actually needed. Avoid `'unsafe-inline'`/`'unsafe-eval'` for scripts. Explicitly allow-list any
  third-party font/style/script origin instead of leaving it broad.
- Set `object-src 'none'`, `base-uri 'self'`, `frame-ancestors 'none'` as safe defaults.
- Treat every new remote resource (script, font, API endpoint) as something that requires an
  explicit CSP and privacy review before being added.
- Set minimal, explicit permissions on any CI workflow token (e.g. GitHub Actions
  `permissions:` block) rather than relying on default broad scopes.

## 4. Security policy documentation

Write a repo-level security policy doc (e.g. `docs/security-policy.md` or `SECURITY.md`) that
covers:

- Core principle: keep the repo secure by default, prefer minimal auditable changes, don't
  bypass existing security automation.
- The exact commands that must pass before a change is considered done (lint, build, test,
  audit) — be concrete, not aspirational.
- Dependency/supply-chain rules (see section 1).
- Secrets/environment rules (see section 2).
- The current control baseline in plain language: what kind of app this is, whether it has a
  backend, what data it stores, what trust boundaries exist.
- A private vulnerability-reporting channel (email or GitHub private advisories) instead of
  asking for public issue disclosure.

**Address this document to AI coding agents explicitly** ("treat as mandatory guidance when
making changes"), not only to humans — agents follow explicit written repo policy far more
reliably than implicit convention, and a CLAUDE.md/AGENTS.md file should point to it.

## Verification checklist

- [ ] Audit tool runs in CI and pre-commit/pre-push, failing on high severity.
- [ ] Lockfile committed and its sync with the manifest is checked in CI.
- [ ] No secrets in git history or the client bundle; `.env.example` exists if env vars are used.
- [ ] If web-facing: CSP is present, reviewed, and as strict as functionality allows.
- [ ] A security policy doc exists, states required checks, and is referenced from the
      agent-facing project doc.
- [ ] Automated dependency updates pass through the same audit/lint/test gate as any other change.
