# Review collaboration contract

This contract applies to every toolkit skill. Specialist skills own their analysis; they do not duplicate another specialist’s full review.

## Evidence labels

Use one of these labels for consequential claims:

- `confirmed`: directly supported by current evidence.
- `inferred`: a reasonable interpretation, not directly proven.
- `unknown`: the evidence is insufficient to form a useful conclusion.
- `needs validation`: a specific confirmation action is available and should be assigned.

For important claims, include the source, confidence (`high`, `medium`, or `low`), and next action when applicable.

## Language and identifiers

- Respond in the user’s language unless they request another language.
- Keep skill names, command identifiers, file paths, code symbols, and artifact field names stable.
- Translate explanations, findings, recommendations, and surrounding documentation naturally; do not translate identifiers in a way that breaks handoffs or traceability.
- When a localized command invokes a canonical skill, preserve the canonical skill name in the handoff or artifact metadata.
- Use the project’s canonical English evidence values (`confirmed`, `inferred`, `unknown`, and `needs validation`) when machine-readable consistency matters; a translated display label may be added alongside it.

## Finding quality

Every negative finding must explain:

1. The observed evidence.
2. The mechanism causing the problem.
3. The affected user, capability, or system.
4. The likely consequence.
5. A proportionate recommendation or validation step.

Do not call a difference in style, framework, naming, or preferred pattern a defect without a concrete consequence.

## Ownership and handoffs

- `project-recovery` owns triage, sequencing, context-warehouse planning, and coordination. It does not replace specialist analysis.
- `product-discovery` owns product intent, users, scope, goals, and critical workflows at a high level.
- `codebase-archaeology` owns factual repository and runtime inventory. It records technical observations but does not judge architecture quality in depth.
- `software-architecture-review` owns design quality, boundaries, coupling, decisions, maintainability, and change risk.
- `security-privacy-reliability` owns threat, privacy, operational resilience, and production-safety analysis.
- `quality-and-test-review` owns test-system effectiveness, coverage evidence, quality gates, and release confidence.
- `ui-ux-review` owns interface usability, accessibility, interaction quality, and user friction.
- `documentation-audit` owns completeness, freshness, contradictions, ownership, and traceability of the documentation set. It consumes specialist reports rather than re-performing their analysis.

When another specialist is needed, record a handoff with:

```text
Handoff to:
Question or risk:
Evidence already collected:
What the receiving skill should assess:
Expected artifact:
```

## Shared scope rules

- Inventorying a concern is different from evaluating it. A skill may record that tests, logs, or accessibility checks exist; the owning specialist evaluates their effectiveness.
- A cross-cutting concern can appear in several reviews, but each review must use its own lens. For example, architecture checks whether observability is structurally supported; reliability checks whether it detects and helps recover from failures; quality checks whether it is tested and gated.
- Do not create a second score for a concern already scored by another skill. Link to the owning report.
- Do not claim security, privacy, accessibility, compliance, reliability, or production readiness from documentation or heuristic review alone.

## Recommended team sequence

1. Project recovery decides whether the full workflow is warranted.
2. Product discovery establishes intent and critical behavior.
3. Codebase archaeology establishes implementation facts.
4. Architecture review assesses design and change risk.
5. Security/privacy/reliability assesses harmful failure and operational risk.
6. Quality review assesses test evidence and release confidence.
7. UI/UX review assesses user-facing quality.
8. Documentation audit reconciles all artifacts and tracks unresolved gaps.

## Soft sequence warnings

Before starting, inspect the project’s available toolkit artifacts and determine which prerequisite context is present. If a recommended prerequisite is missing, begin the response with:

```text
WORKFLOW ORDER WARNING
This review is being run without: [missing artifact or context].
Recommended previous step: [skill].
Effect: [what this review can and cannot conclude without it].
Proceeding because: [user requested this review / urgent isolated review / other reason].
```

Warn, but do not block, unless the user explicitly asks for a strict gate. An urgent or isolated specialist review can be useful without every prior artifact.

Recommended prerequisite checks:

| Skill | Recommended context | Warning when missing |
|---|---|---|
| Product discovery | None | Never warn; this is the starting point. |
| Codebase archaeology | Repository access | Warn that conclusions are limited to supplied artifacts if the repository is unavailable. |
| Architecture review | Product brief and codebase map | Warn that design findings may lack product context or implementation evidence. |
| Security/privacy/reliability | Product scope and codebase/system map | Warn that risk coverage may be incomplete without boundaries, data flows, and runtime context. |
| Quality/test review | Critical workflows and repository map | Warn that test adequacy cannot be judged well without knowing important behavior and test locations. |
| UI/UX review | Target users, critical task, and usable interface evidence | Warn that scoring is provisional when user/task context or representative screens are missing. |
| Documentation audit | Existing docs plus relevant specialist reports | Warn that it is auditing partial evidence and cannot reconcile missing specialist reviews. |

After the warning, continue with the requested work and list the missing prerequisite as a validation action. Do not rely on conversation history as proof that a previous skill was completed; use the artifacts actually available in the project.
