---
name: quality-and-test-review
description: Assess how a software product is tested and how much confidence the test system provides. Inventory unit, integration, contract, end-to-end, mutation, performance, accessibility, security, and other applicable tests; inspect coverage and CI reports; identify gaps, flaky tests, weak quality gates, and untested critical behavior. Use when onboarding to a project or evaluating release readiness.
---

# Quality and test review

Act as a product engineer reviewing the quality system of an existing product. Explain not only what tests exist, but what risks they cover, what they do not cover, and how trustworthy the reports are.

Read [review-contract.md](../../references/review-contract.md) for shared evidence labels and handoff rules.

Before starting, check for critical workflows and a repository map. If they are missing, issue the contract’s soft sequence warning and treat coverage of business-critical behavior as unknown rather than adequate.

## Review workflow

1. Identify critical user journeys, business rules, failure modes, integrations, and quality risks.
2. Inventory test types, frameworks, commands, locations, environments, data, fixtures, and ownership.
3. Inspect CI pipelines, test selection, quality gates, retries, quarantines, artifacts, and reporting.
4. Locate coverage reports and distinguish line, branch, function, statement, path, and meaningful behavioral coverage where available.
5. Review mutation testing, contract testing, performance testing, accessibility testing, security testing, and visual testing when applicable.
6. Check test determinism, isolation, execution time, flaky-test history, false positives, false negatives, and production-like fidelity.
7. Map critical product risks to test evidence and identify confidence gaps.
8. Produce a prioritized improvement plan and the commands or experiments needed to verify it.

Use direct evidence from test files, package scripts, CI configuration, reports, dashboards, test history, incidents, defects, and release records. Do not equate high code coverage with high product quality. Do not invent coverage percentages when reports are unavailable. Inventory security, accessibility, performance, and UX tests, but hand off the effectiveness of those domains to their owning reviews when that is the question.

## Test taxonomy

Classify tests using the project’s own terminology, mapping it to these categories when possible:

- Unit: isolated functions, classes, or modules.
- Component: a deployable or UI component tested with realistic collaborators.
- Integration: multiple real modules, services, databases, or queues working together.
- Contract: compatibility between a producer and consumer of an API or event.
- End-to-end (E2E): a user or external system journey across the deployed product.
- Mutation: deliberate code mutations used to measure whether tests detect behavioral changes.
- Performance: load, stress, soak, spike, volume, latency, and resource tests.
- Accessibility: automated and manual checks for accessible interaction.
- Security: tests for authorization, input handling, abuse cases, dependency risk, and data exposure.
- Visual or snapshot: rendered-output regression checks, including their review process.

Only recommend a category when it addresses a real product risk or an explicit requirement. The appropriate balance depends on the product, architecture, and failure cost.

## Required output

### 1. Quality overview

Summarize the current testing maturity, confidence in the reports, strongest protections, and most important blind spots.

### 2. Test inventory

Use a table with:

```text
Test type:
Purpose:
Scope and critical behavior covered:
Framework and location:
Command:
Environment and dependencies:
Execution frequency:
Owner:
Evidence:
Confidence:
```

### 3. Coverage report

Report available measurements separately:

- Line coverage
- Branch coverage
- Function or method coverage
- Statement coverage
- Mutation score
- Test counts and duration
- Pass, fail, skipped, quarantined, and flaky counts

Include report date, commit or build, scope, exclusions, thresholds, and whether the numbers are reproducible. Explain what the metrics do not measure.

### 4. Critical-behavior matrix

Map important workflows and risks to test types and evidence:

```text
Behavior or risk:
Business impact:
Expected test level:
Existing evidence:
Missing evidence:
Release consequence:
```

### 5. Test-system findings

Identify missing coverage, weak assertions, excessive mocking, brittle fixtures, environment drift, slow feedback, flaky tests, hidden exclusions, unreviewed snapshots, ineffective mutation tests, unrealistic performance tests, and CI/reporting failures.

For each finding, include:

```text
Finding:
Category: coverage | correctness | reliability | speed | maintainability | tooling | process | reporting
Severity: critical | high | medium | low
Evidence:
Why it matters:
Affected behavior:
Recommendation:
Validation method:
Owner type:
Confidence:
```

### 6. Quality gates and release readiness

Document which checks block a release, which are advisory, who can override them, what evidence is retained, and whether rollback or post-release verification exists.

### 7. Prioritized improvement plan

Order improvements by risk reduction and feedback value. Separate immediate fixes, targeted new tests, test-system improvements, and longer-term quality investments.

## Review principles

- A test is valuable when it can detect a meaningful regression at an appropriate cost.
- Coverage metrics are signals, not proof of correctness.
- Critical business rules need assertions that verify outcomes, not merely execution.
- Prefer a small number of trustworthy tests over a large number of redundant or flaky tests.
- Treat skipped, quarantined, and permanently retried tests as visible quality debt.
- Compare test evidence with incidents and escaped defects to find missing test strategies.
- Report unavailable data as unknown rather than estimating it.
