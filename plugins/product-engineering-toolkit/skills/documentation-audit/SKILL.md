---
name: documentation-audit
description: Audit a product's documentation against its repository and supplied evidence, finding missing topics, stale claims, contradictions, ownerless documents, and high-risk unknowns. Use when validating generated documentation, preparing a handoff, or checking whether an undocumented product is understood well enough to change safely.
---

# Documentation audit

Treat documentation as a set of claims that must be checked. Compare documents with implementation and current project evidence rather than judging only writing quality.

Read [review-contract.md](../../references/review-contract.md) for shared evidence labels and handoff rules.

Before starting, check for the existing documentation and the relevant specialist reports. If specialist artifacts are missing, issue the contract’s soft sequence warning and audit the gap rather than silently treating the topic as reviewed.

## Audit dimensions

- Product purpose, users, scope, and success measures.
- Critical workflows, states, permissions, rules, and failure behavior.
- Architecture, data, APIs, integrations, environments, and dependencies.
- Security, privacy, reliability, monitoring, support, deployment, and rollback reports.
- Decisions, risks, unknowns, ownership, verification dates, and links.

## Required output

Return:

1. Covered topics and evidence quality.
2. Missing topics.
3. Contradictions between documents, code, specialist reports, and stakeholder intent.
4. Claims without sufficient evidence.
5. Stale, duplicate, or ownerless documents.
6. Highest-risk documentation gaps.
7. Prioritized remediation plan ordered by user impact, operational risk, and effort.
8. A proposed review cadence.

For every finding include:

```text
Finding:
Severity: critical | high | medium | low
Evidence:
Affected artifact:
Owner type:
Recommended action:
Validation method:
```

Do not re-perform the architecture, security, quality, or UI/UX review. Check whether those specialist artifacts exist, are current, internally consistent, and linked to evidence. Do not claim that a product is compliant, secure, reliable, accessible, or production-ready based only on documentation completeness. Identify what must be verified by the relevant owner.
