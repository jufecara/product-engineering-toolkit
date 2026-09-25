# Product Engineering Toolkit Usage Guide

Use the toolkit as a staged review team. Start broad, collect evidence, then ask specialist skills to evaluate specific dimensions.

For day-to-day product work, use the practice loop first. The staged review team is the assurance path for takeovers, risky changes, and deeper reviews.

## The beginner path

If you are starting as a product engineer, use this progression:

1. **Understand one journey.** Use `product-discovery` and `codebase-archaeology` to map one user goal, one code path, and the current unknowns.
2. **Frame one outcome.** Use `product-engineering-practice` and `templates/outcome-brief.md` before proposing a solution.
3. **Shape a thin slice.** Separate the smallest real user outcome from prototypes, spikes, and deferred scope.
4. **Ship safely.** Use `templates/feature-release-readiness.md` to cover behavior, UX, tests, data, observability, rollout, and rollback.
5. **Learn.** Use `templates/experiment-and-learning-record.md` to record what changed, what the evidence says, and whether to continue, iterate, expand, roll back, or stop.

The goal is not to make every engineer perform every specialist review. The goal is to know enough to make a good first decision and enough to recognize when deeper expertise is needed.

## Day-to-day practice loop

```text
Understand → Frame → Shape → Build → Validate → Release → Learn
```

The loop should produce an outcome brief and a learning record for meaningful changes. Link specialist artifacts to the brief instead of copying their full analysis into every feature document.

## The assurance sequence

```text
Project recovery
      ↓
Product discovery + codebase archaeology
      ↓
Architecture review
      ↓
Security / privacy / reliability review
      ↓
Quality and test review
      ↓
UI/UX review
      ↓
Documentation audit
```

You do not need every stage for every task. Use the sequence when taking ownership of an unfamiliar product.

## Optional command entrypoints

Users who prefer explicit commands can use:

```text
/project-recovery
/product-discovery
/codebase-archaeology
/architecture-review
/security-review
/quality-review
/ui-ux-review
/documentation-audit
```

The standalone hardening/hygiene checklists also have their own command entrypoints, usable independently of the sequence above:

```text
/ci-cd-pipeline
/code-quality-gates
/dependency-management
/pwa-hardening
/repo-hygiene
/security-hardening
/testing-practices
```

These are convenience shortcuts. They do not force the sequence, disable implicit skill selection, or prevent an isolated review. `/project-recovery` is the recommended starting command when taking over an undocumented or drifting project.

Localized aliases are also available in `commands/` for Spanish (`-es`), Portuguese (`-pt`), French (`-fr`), and Italian (`-it`). For example, `/recuperacion-proyecto-es` and `/recuperacao-projeto-pt` both route to the canonical `project-recovery` skill. The language suffix keeps filenames unique where translations share the same words. For natural-language requests, use `locales/registry.json` and `references/language-routing.md` to detect the language, select the appropriate localized resources, and respond in that language.

### Order warnings

The toolkit uses soft sequencing. A skill checks whether its recommended prerequisite artifacts are present and warns when they are missing, but it continues if the user requested an isolated or urgent review. It should explain what conclusions are limited by the missing context. The toolkit checks project artifacts, not conversation history.

## Entry point: project recovery

Use `project-recovery` only at project takeover, after a long period of undocumented change, or when the team has lost confidence in its shared understanding. It first decides whether a full recovery is justified. For a healthy, well-documented project, it should recommend targeted maintenance instead of running every review.

Example request:

```text
Use project-recovery to assess whether this project has lost important context. Inspect the available documentation and repository, classify the recovery need, and propose the smallest useful sequence of specialist reviews.
```

The two foundation reviews—product discovery and codebase archaeology—can run independently or in parallel. The specialist reviews follow once their inputs exist, and documentation audit runs last.

## Step 1: Product discovery

Use when you need to understand what the product is, who it serves, why it exists, and which workflows matter.

Example request:

```text
Use the product-discovery workflow. Understand this product, identify its critical users and workflows, and list the highest-value unknowns before making recommendations.
```

Produces: product brief, users, goals, scope, workflows, domain concepts, constraints, risks, and validation questions.

## Step 2: Codebase archaeology

Use after product discovery to understand how the software actually works.

Example request:

```text
Use codebase-archaeology. Map the repository, runtime, entry points, data stores, integrations, setup, tests, deployment, and one critical workflow end to end.
```

Produces: repository map, architecture facts, flow traces, dependency inventory, setup guide, and technical observations.

This skill records facts. It does not make the final architecture, security, or quality judgment.

## Step 3: Software architecture review

Use when you need to determine whether the design is maintainable and appropriate for the product.

Example request:

```text
Use software-architecture-review with the product brief and codebase map. Identify harmful coupling, weak boundaries, obsolete decisions, unnecessary complexity, and change-risk hotspots. Support every finding with evidence.
```

Produces: architecture map, findings register, decision review, improvement plan, and validation plan.

## Step 4: Security, privacy, and reliability review

Use when the product handles sensitive data, permissions, external dependencies, production traffic, or recovery obligations.

Example request:

```text
Use security-privacy-reliability. Review trust boundaries, sensitive data, access controls, abuse cases, failure modes, backups, recovery, monitoring, and incident readiness. Do not claim compliance or certification.
```

Produces: trust/data-flow summary, security findings, privacy findings, reliability findings, risk register, and production-readiness gaps.

## Step 5: Quality and test review

Use when you need to understand release confidence and how the product is being tested.

Example request:

```text
Use quality-and-test-review. Inventory unit, component, integration, contract, E2E, mutation, performance, accessibility, security, and visual tests. Inspect coverage reports, CI gates, flaky tests, and gaps around critical behavior.
```

Produces: test inventory, coverage report, critical-behavior matrix, quality findings, and release-readiness assessment.

Never invent coverage numbers. Treat unavailable reports as unknown.

## Step 6: UI/UX review

Use when a user-facing workflow, interface, screenshot, prototype, or live product needs evaluation.

Example request:

```text
Use ui-ux-review for the onboarding and checkout journeys. Evaluate the flows at desktop and mobile sizes, score the applicable heuristics, identify accessibility gaps, and recommend improvements.
```

Produces: heuristic scorecard, critical-journey review, accessibility checks, findings, and improvement roadmap.

The score is a consistent triage signal, not proof of user satisfaction or accessibility compliance.

## Step 7: Documentation audit

Use last, after the specialist reviews, to reconcile the documentation with implementation and findings.

Example request:

```text
Use documentation-audit. Compare the product documentation with the repository and specialist reports. Find stale claims, contradictions, missing evidence, ownerless documents, and the highest-risk gaps.
```

Produces: documentation gap report, contradiction list, ownership gaps, remediation plan, and review cadence.

This skill checks specialist reports; it does not replace them.

## How to coordinate the skills

Pass each completed artifact to the next skill. Keep a project folder such as:

```text
docs/product-engineering/
├── 01-product-discovery.md
├── 02-codebase-archaeology.md
├── 03-architecture-review.md
├── 04-security-privacy-reliability.md
├── 05-quality-and-test-review.md
├── 06-ui-ux-review.md
├── 07-documentation-audit.md
├── risks.md
├── decisions.md
└── unknowns.md
```

When handing work between skills, include:

```text
Handoff to:
Question or risk:
Evidence already collected:
What to assess:
Expected artifact:
```

## Practical operating rhythm

- Initial takeover: run all applicable stages.
- Before a major feature: run product discovery, architecture, quality, and UI/UX reviews.
- Before production release: run security/privacy/reliability, quality, and documentation audits.
- After an incident: run archaeology, architecture, security/reliability, and quality reviews.
- Weekly across multiple projects: use the latest risks, unknowns, decisions, and next actions to create a portfolio status brief.

Always finish with three lists: what is known, what is unknown, and what must happen next.
