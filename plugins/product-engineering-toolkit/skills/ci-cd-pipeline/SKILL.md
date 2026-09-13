---
name: ci-cd-pipeline
description: "CI/CD pipeline structure for any project: layered PR-check gates, a stricter deploy workflow, static analysis (SAST) scanning, and minimal token permissions. Use when setting up CI from scratch, or reviewing/hardening an existing pipeline that's missing gates or over-scoped permissions."
risk: safe
source: personal
date_added: "2026-09-13"
---

# CI/CD Pipeline

> Stack-agnostic; examples use GitHub Actions syntax but the structure applies to any CI system
> (GitLab CI, CircleCI, Jenkins, etc.).

## 1. Separate "PR checks" from "deploy"

- **PR-check workflow**: triggers on every pull request into the integration/default branch.
  Runs the full validation gate (see below) and nothing else — no deploy, no publish.
- **Deploy workflow**: triggers only on push to the release branch (or a tag). Re-runs the same
  validation gates from scratch — never assume "PR checks already passed" is enough, since
  direct pushes or admin merges can bypass branch protection. Only after every gate passes does
  it build and deploy.
- Use `concurrency` groups on the deploy workflow so overlapping deploys don't race each other.

## 2. Ordered validation gates

Run cheap/fast checks before expensive ones so a pipeline fails fast:

1. Install dependencies with a frozen/reproducible install command (`npm ci`, `pip install -r
   requirements.txt --no-deps` with a lock, `bundle install --frozen`, etc.) — never a command
   that can silently update the lockfile.
2. Security/dependency audit.
3. Lint.
4. Format check.
5. Lockfile-sync check (diff the lockfile post-install; fail if dirty) — catches manifests and
   lockfiles that drifted apart.
6. Type check (if applicable).
7. Test suite (+ coverage report on the deploy workflow, if not on every PR for speed).
8. Build.
9. (Deploy workflow only) Publish/deploy artifact.

## 3. Static analysis (SAST)

- Add a static analysis tool (CodeQL, Semgrep, or the language's equivalent) that runs on push
  and PR to protected branches, plus a weekly scheduled scan to catch newly disclosed rule
  patterns against unchanged code.
- Give its workflow only the permissions it needs (`security-events: write`, `contents: read`,
  `actions: read` — nothing broader).

## 4. Minimal permissions everywhere

- Every workflow declares an explicit `permissions:` block instead of relying on the default
  (which is often broader than needed). Start from `contents: read` and add only what a specific
  job requires (`pages: write`, `id-token: write` for OIDC deploys, `issues: write` for bot
  automation, etc.).

## 5. Bot/automation hygiene

- If using a dependency bot (Dependabot/Renovate), route its PRs through the same PR-check
  workflow as any human PR — a bot-authored change gets no exemption from the gate.
- Add a follow-up workflow that watches the PR-check workflow's result and automatically closes
  (with an explanatory comment) any bot-authored PR that fails CI, so broken automated bumps
  don't sit unresolved. (Scheduling, labeling, and capping the bot itself is configuration, not
  pipeline structure — covered here only insofar as its output must pass through this gate.)

## Verification checklist

- [ ] PR-check workflow exists and blocks merge on failure (branch protection configured).
- [ ] Deploy workflow re-runs full validation, doesn't just trust the PR check.
- [ ] Lockfile-sync check exists somewhere in the pipeline.
- [ ] SAST scanning configured with scheduled + on-push/PR triggers.
- [ ] Every workflow has an explicit, minimal `permissions:` block.
- [ ] Dependency bot PRs run through the same PR-check gate and are auto-closed on CI failure.
