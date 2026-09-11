---
name: product-discovery
description: Understand an undocumented software product and turn available code, tickets, notes, and stakeholder context into an evidence-backed product brief, workflow map, constraint register, risk register, and prioritized documentation plan. Use when onboarding to a product, taking over a project, or asking what a product does and how it works.
---

# Product discovery

Act as a senior product engineer joining an undocumented product. Your job is to build a useful working model while preserving uncertainty.

Read [review-contract.md](../../references/review-contract.md) for shared evidence labels and handoff rules.

This is the starting workflow, so it does not require a prior toolkit artifact. If the user asks for a narrow discovery slice, state what broader product context remains unknown.

## Workflow

1. Inventory the supplied material and identify missing evidence.
2. Establish product purpose, users, value, success measures, and scope.
3. Identify critical workflows, actors, permissions, states, business rules, and side effects.
4. Identify technical boundaries, important data, integrations, environments, and operational dependencies at a product level.
5. Extract product constraints, risks, decisions, contradictions, and unknowns; hand off deep technical reviews to the appropriate specialist.
6. Produce the artifacts below and end with the smallest next validation actions.

Do not invent requirements or present implementation details as product intent. If evidence conflicts, show both interpretations and explain what would resolve the conflict.

## Required output

Return these sections:

1. Executive product brief.
2. Users, roles, and critical jobs to be done.
3. Critical workflow summary, including alternate and failure paths.
4. Domain concepts and important state transitions.
5. Rules and constraints register.
6. System and integration map.
7. Risks, contradictions, and unknowns.
8. Recommended documentation tree.
9. Prioritized next actions with owner type, evidence needed, and expected outcome.

For consequential claims, use the shared evidence labels and source/confidence format from the review contract.

## Project handoff questions

Ask only questions that cannot be answered safely from the supplied material. Prioritize questions about product intent, user impact, irreversible decisions, security/privacy, operational safety, and conflicting rules.

Do not perform the architecture, security, test, or UI/UX specialist reviews here. Identify the question and create a handoff for the relevant skill.

## Completion criteria

The discovery is useful when a new contributor can explain what the product does, who it serves, how its main workflows behave, which rules constrain changes, what remains unknown, and what should be investigated next.
