# Product Engineering Toolkit for Claude Code

Use this project as a reusable product-engineering workflow when taking ownership of an undocumented software product.

## Operating principles

- Inspect the repository and supplied evidence before forming conclusions.
- Separate product intent from implementation behavior.
- Never turn an assumption into a requirement.
- Label consequential findings as `confirmed`, `inferred`, `unknown`, or `needs validation`.
- Cite evidence using file paths, symbols, tests, tickets, interviews, metrics, or commands.
- Never expose secret values; report only configuration names and their purpose.
- Do not modify code or create documentation files unless the user asks for that action.
- When evidence conflicts, show the conflict and identify the smallest validation step.
- Respond in the user’s language while keeping skill names, command identifiers, file paths, code symbols, and artifact field names stable.

## Choose the workflow

Use the relevant instruction file below as the detailed workflow. Read it before performing that kind of work:

First read `references/review-contract.md` when coordinating two or more toolkit workflows.
Use `USAGE_GUIDE.md` for the overall sequence and handoff format.

- Product understanding and onboarding: `skills/product-discovery/SKILL.md`
- Project recovery and workflow coordination: `skills/project-recovery/SKILL.md`
- Repository and architecture investigation: `skills/codebase-archaeology/SKILL.md`
- Architecture quality and design review: `skills/software-architecture-review/SKILL.md`
- Test strategy and quality review: `skills/quality-and-test-review/SKILL.md`
- UI/UX heuristic evaluation: `skills/ui-ux-review/SKILL.md`
- Documentation quality and completeness review: `skills/documentation-audit/SKILL.md`
- Security, privacy, and reliability review: `skills/security-privacy-reliability/SKILL.md`

If more than one workflow applies, use them in this order:

1. `project-recovery` when taking over an undocumented or drifting project
2. `product-discovery` and `codebase-archaeology`
3. `software-architecture-review` when design quality, technical debt, or change risk is in scope
4. `security-privacy-reliability` when risk or production readiness is in scope
5. `quality-and-test-review` when test strategy, coverage, or release confidence is in scope
6. `ui-ux-review` when usability, accessibility, interface quality, or user friction is in scope
7. `documentation-audit`

## Hardening and hygiene checklists

Each of these is a standalone, stack-agnostic checklist — use any one in isolation for setup or
review work; they don't need to be chained together or read in sequence:

- CI/CD pipeline structure and gating: `skills/ci-cd-pipeline/SKILL.md`
- Formatter/linter/pre-commit enforcement: `skills/code-quality-gates/SKILL.md`
- Dependency and lockfile hygiene: `skills/dependency-management/SKILL.md`
- Service worker / installable-app hardening (PWAs only): `skills/pwa-hardening/SKILL.md`
- Repository and contributor-experience hygiene: `skills/repo-hygiene/SKILL.md`
- Security and supply-chain hardening: `skills/security-hardening/SKILL.md`
- Test suite conventions and coverage: `skills/testing-practices/SKILL.md`

## Required output quality

Every discovery or audit result must include:

1. What is known.
2. What is inferred.
3. What remains unknown.
4. Contradictions and risks.
5. The next smallest validation actions.

For important claims, use this format:

```text
Status: confirmed | inferred | unknown | needs validation
Source: file, symbol, test, ticket, interview, metric, command, or supplied artifact
Confidence: high | medium | low
```

## Suggested requests

```text
Use the product-discovery workflow to understand this product. Start by inspecting the repository and identify the highest-value unknowns before writing the product brief.
```

```text
Use the codebase-archaeology workflow to map the repository, trace one critical workflow end to end, and document setup, testing, deployment, integrations, and technical risks.
```

```text
Use the documentation-audit workflow to compare the current docs with the repository and identify stale claims, contradictions, missing topics, and the highest-risk gaps.
```

## Templates

Reusable templates are available in:

- `templates/evidence-record.md`
- `templates/risk-record.md`

When working in a separate product repository, copy this `CLAUDE.md`, the required skill files, and any templates into that repository, or adjust the paths above to match the local layout.
