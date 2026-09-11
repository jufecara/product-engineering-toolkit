---
name: codebase-archaeology
description: Reverse-engineer an unfamiliar software repository into an evidence-backed architecture map, runtime/setup guide, request and job flows, data/integration inventory, test assessment, and technical risk list. Use when a repository lacks documentation or when taking ownership of an existing codebase.
---

# Codebase archaeology

Inspect the repository as a product engineer. Prefer direct evidence from files, tests, scripts, configuration, migrations, logs, and safe execution over assumptions.

Read [review-contract.md](../../references/review-contract.md) for shared evidence labels and handoff rules.

Before starting, apply the contract’s soft sequence warning if repository access or sufficient source material is unavailable.

## Workflow

1. Identify repository boundaries, languages, runtimes, package managers, and deployable units.
2. Locate entry points, routes, commands, workers, scheduled jobs, event handlers, and migrations.
3. Trace one representative user or system flow end to end.
4. Map persistence, external services, authentication, configuration, and environment differences.
5. Inspect tests, validation, error handling, observability, build, release, and rollback paths.
6. Identify duplicated behavior, dead code, temporary workarounds, dangerous defaults, and undocumented coupling as observations for specialist review.

Never expose secret values. Report secret names and configuration purpose only. Do not modify code unless explicitly asked.

## Required output

1. Repository purpose and boundaries.
2. Architecture overview in plain language.
3. Important directories, symbols, and entry points.
4. Runtime and dependency inventory.
5. Request, event, and background-job flows.
6. Data stores, schemas, migrations, and ownership.
7. External integrations and failure behavior.
8. Local setup, quality checks, release, and rollback instructions.
9. Test strategy and coverage gaps.
10. Technical observations, risks, and questions for specialist review.

Support important findings with a path, symbol, command, test, or configuration reference. Label each finding `confirmed`, `inferred`, `unknown`, or `needs validation`.

Do not issue a deep architecture-quality judgment, security assessment, test-quality assessment, or reliability certification. Record the evidence and hand off those questions to `software-architecture-review`, `security-privacy-reliability`, or `quality-and-test-review`.

## Completion criteria

The archaeology is useful when a new engineer can run the system safely, find the code for a critical workflow, understand its data and dependencies, execute quality checks, and recognize the main risks before making a change.
