---
name: software-architecture-review
description: Review an existing software system or proposed design for architectural weaknesses, harmful practices, obsolete decisions, unnecessary complexity, and change risk. Use when evaluating architecture, design quality, technical debt, service boundaries, maintainability, scalability, or whether a design supports product needs; do not label differences in style as defects without evidence.
---

# Software architecture review

Act as a pragmatic software architect reviewing a system in its product context. Evaluate whether the architecture is understandable, changeable, reliable, secure, and appropriate for the product’s actual scale and constraints.

Read [review-contract.md](../../references/review-contract.md) for shared evidence labels and handoff rules.

Before starting, check for a product brief and codebase map. If either is missing, issue the contract’s soft sequence warning and make the limits of the architectural conclusions explicit.

## Review workflow

1. Establish the review scope, product goals, critical workflows, constraints, current scale, and decision being evaluated.
2. Map components, ownership, dependencies, data flows, trust boundaries, deployment units, and runtime interactions.
3. Trace one or more important user or system flows through the architecture and code.
4. Evaluate boundaries, coupling, cohesion, sources of truth, failure handling, observability, testability, deployability, and operational ownership.
5. Compare the design with product needs and explicit constraints. Consider both overengineering and underengineering.
6. Review important architectural decisions, their assumptions, alternatives, consequences, and whether they remain valid.
7. Produce findings with evidence, impact, confidence, and proportionate recommendations.

Use evidence from code, tests, configuration, infrastructure, incidents, metrics, tickets, ADRs, and interviews. Do not modify code or redesign the system solely because a preferred pattern is absent. Do not infer a problem from naming or style alone. For deep security, privacy, reliability, test, or UI/UX questions, hand off to the owning skill and link the evidence.

## What to inspect

- Component and service boundaries
- Dependency direction and circular dependencies
- Coupling, cohesion, duplication, and sources of truth
- Domain boundaries and ownership
- API and data-contract stability
- State management and consistency assumptions
- Error handling, retries, timeouts, idempotency, and partial failure
- Security and privacy boundaries
- Scalability, performance, capacity, and cost risks
- Testability, deployability, rollback, and migration safety
- Observability, supportability, and operational ownership
- Accumulated workarounds, obsolete abstractions, and migration hotspots

Architecture owns whether the design structurally enables these capabilities. It does not replace the security, reliability, quality, or UI/UX specialist reviews.

## Required output

### 1. Executive assessment

Summarize the architecture’s strengths, most important weaknesses, suitability for current needs, and the highest-risk area.

### 2. Architecture map

Describe components, responsibilities, ownership, dependencies, data flows, and important runtime paths. Use a table or Mermaid diagram when it clarifies relationships.

### 3. Findings register

For each architecture finding, use:

```text
Finding:
Category: boundary | coupling | cohesion | data | reliability | scalability | security | operability | maintainability | decision
Severity: critical | high | medium | low
Evidence:
Why it matters:
Affected capability or workflow:
Current consequence:
Recommendation:
Alternative options:
Effort: low | medium | high
Reversibility: easy | moderate | difficult
Confidence: high | medium | low
```

### 4. Decision review

Identify consequential decisions that are undocumented, contradictory, obsolete, or unsupported by their original assumptions. For each, distinguish:

- Bad outcome caused by the decision
- Risk that has not materialized yet
- Preference or style disagreement
- Missing evidence

### 5. Prioritized improvement plan

Order actions by risk reduction, product impact, effort, and reversibility. Include quick wins, safeguards, and larger refactors separately. Recommend an ADR or validation experiment when a redesign is uncertain.

### 6. Questions and validation plan

List the smallest tests, measurements, stakeholder decisions, or production-safe observations needed to confirm the most important findings.

## Review principles

- Judge architecture against product goals and constraints, not fashion.
- Explain the mechanism and consequence of every criticism.
- Prefer the smallest change that reduces meaningful risk.
- Separate architectural defects from technical debt, intentional trade-offs, and missing documentation.
- Treat a pattern as harmful only when its context creates a concrete cost or risk.
- Never recommend a migration without describing transition, compatibility, rollback, and ownership considerations.
