# Product Engineering Toolkit Usage Guide

Use the toolkit as a staged review team. Start broad, collect evidence, then ask specialist skills to evaluate specific dimensions.

## The standard sequence

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

These are convenience shortcuts. They do not force the sequence, disable implicit skill selection, or prevent an isolated review. `/project-recovery` is the recommended starting command when taking over an undocumented or drifting project.

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
