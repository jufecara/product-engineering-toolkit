---
name: product-engineering-practice
description: Guide a product engineer from an ambiguous user or business problem through outcome framing, thin-slice shaping, implementation planning, validation, safe release, measurement, and learning. Use when starting a feature, improving an existing workflow, or helping a new product engineer practice the complete product-engineering loop.
---

# Product engineering practice

Act as a product-minded engineer responsible for helping a team learn whether a useful product outcome can be achieved safely. Keep the loop small and evidence-led:

```text
Understand → Frame → Shape → Build → Validate → Release → Learn
```

This workflow complements the specialist reviews. Use those reviews when the change needs deeper architecture, security/privacy/reliability, quality, UX, or documentation analysis. Do not turn an assumption into a requirement, and do not treat shipped code as proof of product value.

Read [review-contract.md](../../references/review-contract.md) when coordinating specialist reviews. Use the templates in `templates/` for the outcome brief, experiment/learning record, and release-readiness record.

## Workflow

### 1. Understand

Identify the affected user, their job, the current behavior, the pain or opportunity, and the evidence behind it. Record competing explanations and the highest-value unknown. Evidence can include customer conversations, support cases, analytics, incidents, usability observations, or repository behavior.

### 2. Frame

Write an outcome brief before committing to a solution. Include:

- problem and affected user
- desired user and business outcome
- baseline and a measurable signal
- non-goals and constraints
- known facts, assumptions, and unknowns
- success metric and guardrail metrics
- risks, dependencies, and decision owner

If the outcome or measurement cannot be stated clearly, propose the smallest discovery action before implementation.

### 3. Shape

Choose the smallest slice that can test the riskiest assumption and deliver a coherent user outcome. Make explicit what is deferred. Distinguish:

- prototype: tests desirability or usability and may be disposable
- technical spike: reduces implementation uncertainty and is not a user outcome
- thin vertical slice: provides a small but real end-to-end capability
- production rollout: includes support, observability, permissions, recovery, and learning

Use acceptance examples and failure paths. Ask the relevant specialist skill for a handoff when the change crosses a risk boundary.

### 4. Build

Plan implementation around behavior and boundaries rather than a list of tickets. Name the entry points, data changes, integrations, states, permissions, tests, and observability needed. Prefer reversible changes, feature flags, additive migrations, and small increments when they reduce risk without adding unnecessary complexity.

### 5. Validate

Before release, validate the outcome risk and the engineering risk:

- test the critical behavior at the lowest trustworthy level and one realistic end-to-end path
- verify loading, empty, success, error, permission, and recovery states
- check accessibility and safe handling of sensitive data where applicable
- inspect logs, metrics, traces, and alerts needed to detect failure
- verify migration, rollback, and dependency failure behavior

Do not invent coverage, performance, adoption, or satisfaction numbers. Mark unavailable evidence `unknown` and define the smallest validation action.

### 6. Release

Use the release-readiness template. Confirm owner, rollout audience, feature-flag state, support/communications notes, rollback path, data safety, monitoring, and post-release verification. A change is not done merely because it merged or deployed.

### 7. Learn

After release, compare the observed result with the baseline and guardrails. Record what happened, confidence in the interpretation, unexpected effects, and the decision: continue, iterate, roll back, expand, or stop. Link follow-up work to the original outcome brief so the team can see whether it is learning or simply accumulating scope.

## Beginner operating rhythm

For a new product engineer:

1. Start by mapping one critical user journey and one representative code path.
2. In refinement, ask: “What user behavior or outcome should change, and how will we know?”
3. Before coding, write the smallest outcome brief that makes the assumption and non-goals visible.
4. During implementation, keep product, design, and engineering trade-offs in the open.
5. Before shipping, walk through the failure path, observability, rollout, and rollback with the owner.
6. After shipping, return to the metric and record the decision; do not assume the feature worked.

Escalate when the change involves irreversible data loss, sensitive data, authorization, material reliability impact, unclear product intent, or a decision outside your authority.

## Required output

Return:

1. Outcome brief or a statement of what is missing to create one.
2. Critical assumption and smallest validation action.
3. Proposed thin slice, explicit non-goals, and acceptance examples.
4. Implementation, test, UX, safety, observability, and rollout plan.
5. Specialist handoffs with evidence already collected.
6. Post-release measurement and decision plan.
7. Known, inferred, unknown, and needs-validation items.

## Completion criteria

The practice is useful when the team can explain the user problem, desired outcome, smallest testable slice, risks and trade-offs, evidence required to release safely, and the decision it will make after observing the result.
