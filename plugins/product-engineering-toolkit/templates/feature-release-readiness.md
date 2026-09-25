# Feature release readiness

**Feature or change:**  
**Owner:**  
**Target release:**  
**Rollout strategy:**  

Mark each item `confirmed`, `needs validation`, `unknown`, or `not applicable`. Link evidence for anything material.

## Product and UX

- [ ] User problem, desired outcome, non-goals, and success measure are documented.
- [ ] Acceptance examples cover the main path and important alternate paths.
- [ ] Empty, loading, success, error, disabled, permission, and recovery states are handled.
- [ ] Terminology, accessibility, responsive behavior, and destructive actions were checked.

## Engineering and quality

- [ ] Critical behavior has trustworthy tests at appropriate levels.
- [ ] Integration and end-to-end behavior is covered where failure cost warrants it.
- [ ] Data migrations are backward-compatible or have a verified transition plan.
- [ ] Dependencies, performance risks, and failure behavior are understood.

## Security, privacy, and reliability

- [ ] Authorization and trust-boundary changes were reviewed.
- [ ] Sensitive data collection, storage, logging, and retention were checked.
- [ ] Rate limits, abuse cases, idempotency, and safe retries were considered where applicable.
- [ ] Logs, metrics, traces, alerts, and ownership can detect harmful failure.
- [ ] Backup, recovery, rollback, and degraded-dependency behavior are understood where applicable.

## Release and learning

- [ ] Rollout audience, feature flag, and rollback trigger are owned.
- [ ] Support, communications, and runbook updates are complete where needed.
- [ ] Post-release verification time and owner are scheduled.
- [ ] Experiment or learning record links to the outcome brief.

## Decision

- Release: yes | no | needs validation
- Decision owner:
- Blocking risks:
- Evidence still needed:
