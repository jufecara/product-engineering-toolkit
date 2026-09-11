---
name: ui-ux-review
description: Evaluate a software product’s user experience and interface against evidence-based usability, accessibility, interaction, content, responsive, and visual-design practices. Produce a transparent heuristic score, prioritized findings, and concrete improvements. Use for onboarding audits, feature reviews, screenshots, live interfaces, or critical user journeys; do not present the score as a substitute for user research.
---

# UI/UX review

Act as a pragmatic UX evaluator and product engineer. Assess whether users can understand, navigate, operate, and recover from the product successfully. Make subjective judgments transparent by tying them to observable evidence, recognized heuristics, user goals, and product context.

Read [review-contract.md](../../references/review-contract.md) for shared evidence labels and handoff rules.

Before starting, check for target users, a critical task, and representative interface evidence. If any are missing, issue the contract’s soft sequence warning and keep the score provisional.

## Review workflow

1. Establish the target users, critical tasks, device/context, business goal, and evidence available.
2. Inspect the relevant screens, flows, components, content, interaction states, and implementation. If the product is runnable, exercise the critical journey at representative viewport sizes.
3. Evaluate first-use clarity, information architecture, navigation, visual hierarchy, interaction affordances, feedback, forms, errors, recovery, content, consistency, responsiveness, accessibility, trust, and efficiency.
4. Check meaningful states: loading, empty, success, error, disabled, partial completion, offline or degraded dependency, permission denied, and destructive actions.
5. Score each dimension with evidence and confidence. Do not score unavailable evidence as good.
6. Prioritize improvements by user impact, frequency, severity, effort, and confidence.
7. Separate heuristic findings from findings that require user research, analytics, usability testing, or domain-owner validation.

## Heuristic score

Use a 0–4 scale for each dimension:

```text
0 = absent, blocked, or harmful
1 = serious gap; users are likely to struggle
2 = partially works but has meaningful friction or inconsistency
3 = generally effective with minor issues
4 = strong and deliberate evidence of good practice
N/A = insufficient evidence; exclude from the average
```

Score these dimensions:

- Task clarity and value communication
- Information architecture and findability
- Navigation and wayfinding
- Interaction affordances and consistency
- Feedback, system status, and recovery
- Forms, input, validation, and error prevention
- Content clarity and terminology
- Visual hierarchy and legibility
- Accessibility and inclusive interaction
- Responsive behavior and device suitability
- Performance perception and waiting experience
- Trust, privacy communication, and safe destructive actions
- Efficiency for frequent or expert users

Calculate:

```text
UX heuristic score = (sum of applicable dimension scores / (4 × number of applicable dimensions)) × 100
```

Report the score with the number of dimensions assessed, evidence quality, and confidence. Suggested interpretation:

- 0–39: critical usability risk
- 40–59: substantial friction
- 60–74: usable but inconsistent or opportunity-rich
- 75–89: strong with targeted improvements
- 90–100: excellent heuristic performance, still requiring user validation

These bands are a triage aid, not an industry-standard user-experience metric. Never claim that a score proves users are satisfied or that the product is accessible.

UI/UX owns the user-facing experience of trust, privacy communication, and safe interaction. It does not assess backend privacy controls, security posture, reliability, or test-system effectiveness; hand those questions to the owning skills.

## Required output

### 1. Evaluation context

State users, tasks, surfaces, viewports, evidence, assumptions, and limitations.

### 2. Scorecard

Use:

```text
Dimension:
Score: 0 | 1 | 2 | 3 | 4 | N/A
Evidence:
User impact:
Confidence: high | medium | low
```

Include the overall score and explain excluded dimensions.

### 3. Critical journey review

For each task, describe the intended path, observed path, friction points, recovery options, and likely completion risks.

### 4. Findings register

For each finding, include:

```text
Finding:
Category: clarity | navigation | interaction | content | accessibility | responsive | feedback | form | performance | trust | consistency
Severity: blocker | high | medium | low
Evidence:
Affected users and task:
Why it matters:
Recommendation:
Example improved behavior or copy:
Effort: low | medium | high
Validation method:
Confidence:
```

### 5. Accessibility checks

Check keyboard access, focus visibility and order, semantic structure, labels, contrast, text resizing, target size, motion, screen-reader meaning, error identification, and non-color cues. Mark items requiring automated tooling or manual assistive-technology testing.

### 6. Improvement roadmap

Group recommendations into immediate usability fixes, component/design-system improvements, deeper flow changes, and research questions. Prioritize high-impact, frequent, low-effort changes first unless a blocker requires immediate attention.

## Review principles

- Evaluate against user goals and context, not personal taste.
- Give evidence for every negative judgment.
- Treat accessibility and error recovery as core quality, not optional polish.
- Inspect all important interaction states, not only the happy-path screenshot.
- Prefer specific behavioral recommendations over vague advice such as “make it cleaner.”
- A heuristic review identifies likely problems; user research and product analytics establish whether those problems affect real users.
