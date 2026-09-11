---
name: security-privacy-reliability
description: Review a software product or feature for security, privacy, and operational reliability risks, then produce evidence-backed registers and a validation plan. Use for threat modeling, sensitive-data review, access-control analysis, incident readiness, backup/recovery, observability, or production-readiness assessment; do not use as a substitute for formal compliance or penetration testing.
---

# Security, privacy, and reliability review

Act as a product engineer performing a bounded risk review. The goal is to expose important risks and define verifiable next actions, not to certify the product.

Read [review-contract.md](../../references/review-contract.md) for shared evidence labels and handoff rules.

Before starting, check for product scope, system boundaries, data flows, and runtime evidence. If important context is missing, issue the contract’s soft sequence warning and narrow the review claims accordingly.

## Review workflow

1. Establish scope, system boundaries, environments, users, roles, and review evidence.
2. Map trust boundaries, assets, sensitive data, data flows, and external dependencies.
3. Review authentication, authorization, tenancy isolation, secrets, encryption, input handling, logging, and auditability.
4. Review collection, purpose, access, retention, correction, export, deletion, and sharing of personal or sensitive data.
5. Review availability, failure modes, retries, timeouts, queues, idempotency, backups, recovery, capacity, monitoring, and alerting.
6. Consider abuse cases, accidental misuse, dependency failure, operator error, data corruption, and partial completion.
7. Produce prioritized risks and the smallest useful validation or mitigation for each.

Use direct evidence from code, configuration, tests, infrastructure, logs, incidents, policies, tickets, and interviews. Report secret names or configuration keys, never secret values. Do not exploit systems, access production data, or make security changes unless explicitly authorized. Inventory test and architecture evidence when relevant, but hand off test effectiveness to `quality-and-test-review` and design quality to `software-architecture-review`.

## Required output

### 1. Scope and confidence

State what was reviewed, what was unavailable, and which conclusions are limited by missing evidence.

### 2. Trust-boundary and data-flow summary

Describe actors, services, stores, integrations, boundaries, sensitive assets, and movement of data. Use a table or Mermaid diagram when it makes relationships clearer.

### 3. Security findings

Cover identity, access control, tenant isolation, input/output handling, secrets, encryption, logging, audit trails, dependencies, and abuse cases.

### 4. Privacy findings

Cover data categories, purpose, minimization, access, retention, deletion, exports, sharing, observability exposure, and unresolved policy questions. Do not infer legal obligations without an authoritative policy or qualified owner.

### 5. Reliability findings

Cover critical dependencies, failure modes, recovery behavior, backups, restore testing, monitoring, alerting, capacity, deployment, rollback, and incident response.

### 6. Prioritized risk register

For every risk, include:

```text
Risk:
Category: security | privacy | reliability
Severity: critical | high | medium | low
Cause:
Affected users or systems:
Evidence:
Existing controls:
Detection:
Mitigation or validation:
Owner type:
Status: open | accepted | mitigated | closed
```

### 7. Production-readiness gaps

List missing controls, tests, documentation, ownership, metrics, runbooks, or approvals. Distinguish “not documented” from “not implemented” and “not verified.”

### 8. Next actions

Order actions by risk reduction and effort. Include the expected evidence or decision that would close each action.

## Safety and scope boundaries

- Do not claim the product is secure, private, compliant, or production-ready based on this review.
- Do not invent threat actors, policies, service-level objectives, or regulatory requirements.
- Escalate critical findings involving active exposure, destructive data loss, credential compromise, or inability to recover safely.
- Treat security, privacy, and reliability as ongoing ownership responsibilities, not a one-time checklist.
