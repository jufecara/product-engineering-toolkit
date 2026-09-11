---
name: project-recovery
description: Triage a software project that is undocumented, poorly understood, or drifting from its intended path; decide whether a documentation-recovery review is worthwhile, coordinate the toolkit’s specialist skills, and establish a trustworthy context warehouse for humans and agents. Use at the beginning of a takeover or when project context has been lost, not for routine feature work in a healthy documented project.
---

# Project recovery

Act as the lead product engineer restoring shared context to a project. The objective is not to produce documentation for its own sake; it is to reduce dangerous unknowns and make future product and engineering decisions easier.

Read [review-contract.md](../../references/review-contract.md) and [USAGE_GUIDE.md](../../USAGE_GUIDE.md) before coordinating specialist workflows.

## Phase 1: Decide whether recovery is needed

Inspect the repository and existing project artifacts. Assess whether the project has usable evidence for:

- Product purpose, users, scope, and success measures
- Critical workflows and business rules
- Architecture and system boundaries
- Security, privacy, reliability, and operational ownership
- Test strategy, coverage, and release confidence
- UI/UX quality for critical user journeys
- Decisions, risks, unknowns, and documentation ownership

Classify the project as:

- `healthy`: documentation is current and supported by evidence; recommend targeted maintenance instead of full recovery.
- `recoverable`: important context is missing or stale; run the relevant specialist reviews.
- `high risk`: critical behavior, security, reliability, ownership, or recovery information is unknown; prioritize human validation before risky changes.

Do not use a numerical score as a substitute for judgment. Explain the evidence behind the classification.

## Phase 2: Build the recovery plan

Produce a plan with:

1. Existing artifacts and their freshness.
2. Known, inferred, unknown, and needs-validation items.
3. Critical user journeys and system capabilities.
4. Missing specialist reviews.
5. Recommended skill sequence.
6. Stakeholders and decisions requiring human input.
7. Proposed context-warehouse structure.
8. Stop conditions for unsafe or high-impact work.

Use this default sequence, adapting when urgency or available evidence justifies it:

1. `product-discovery` and `codebase-archaeology` can run independently or in parallel.
2. `software-architecture-review` uses their outputs.
3. `security-privacy-reliability`, `quality-and-test-review`, and `ui-ux-review` can run in parallel once their required context is available.
4. `documentation-audit` reconciles the outputs last.

## Phase 3: Coordinate outputs

For each selected skill, define:

```text
Skill:
Reason selected:
Inputs available:
Expected artifact:
Questions to answer:
Owner or reviewer:
```

Do not repeat a specialist review inside this skill. Coordinate, summarize, identify conflicts, and route questions to the correct owner.

## Phase 4: Define the context warehouse

Recommend or create, when explicitly requested, a project documentation structure containing:

- Product brief
- Users, roles, and critical workflows
- Domain model and business rules
- Repository and architecture map
- Security, privacy, and reliability review
- Quality and test review
- UI/UX review
- Decisions and ADRs
- Risks and unknowns
- Operations and release information
- Documentation index with owners and verification dates

Every artifact should preserve source evidence, confidence, owner, last verification date, and next validation action.

## Required output

Return:

1. Recovery-needed classification with evidence.
2. Current context inventory.
3. Highest-risk gaps.
4. Recommended specialist skills and sequence.
5. Human decisions and interviews needed.
6. Context-warehouse structure.
7. First milestone and definition of done.

If the project is `healthy`, say so clearly and recommend only the smallest targeted review or maintenance action.
