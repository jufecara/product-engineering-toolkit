# Product Engineering Toolkit

A skills-first toolkit for understanding undocumented software products, producing trustworthy documentation, and maintaining project context over time.

The toolkit includes a `CLAUDE.md` adapter for Claude Code. The Codex plugin manifest remains in `.codex-plugin/plugin.json`; Claude Code uses the adapter and the plain Markdown workflow files instead of that manifest.

The shared collaboration rules are in `references/review-contract.md`. Specialist skills should produce their own findings and hand off adjacent concerns instead of duplicating another specialist’s review.

See `USAGE_GUIDE.md` for the recommended sequence, example requests, handoffs, artifacts, and operating rhythm.

The optional `commands/` directory provides explicit command entrypoints for users who prefer them. Commands are shortcuts into skills; they do not replace natural-language requests or automatic skill selection.

Localized command aliases are available for Spanish, Portuguese, French, and Italian. They invoke the same canonical English skills, so findings and handoffs remain traceable while explanations can follow the user’s language.

## Included skills

- `project-recovery`: Decide whether a project needs context recovery and coordinate the specialist workflow.
- `product-discovery`: Establish product purpose, users, workflows, rules, constraints, risks, and unknowns.
- `codebase-archaeology`: Inspect an unfamiliar repository and produce an evidence-backed technical map.
- `software-architecture-review`: Evaluate boundaries, coupling, design decisions, technical debt, and change risk in product context.
- `quality-and-test-review`: Inventory tests, coverage, mutation, performance, CI quality gates, flakiness, and confidence gaps.
- `ui-ux-review`: Evaluate usability, accessibility, interaction quality, responsive behavior, and user friction with a transparent heuristic score.
- `documentation-audit`: Check documentation against evidence, identify contradictions, and prioritize gaps.
- `security-privacy-reliability`: Review trust boundaries, sensitive data, access controls, failure modes, recovery, and operational readiness.

## Evidence standard

Every important claim should be labeled `confirmed`, `inferred`, `unknown`, or `needs validation`, with a source and a next action where applicable. Generated documentation is a working model until reviewed by the appropriate product or technical owner.

## Planned extensions

Potential future skills include workflow modeling, domain rules, API documentation, decision records, risk review, release readiness, and portfolio status.

## Claude Code usage

Copy `CLAUDE.md`, the relevant files under `skills/`, and any needed files under `templates/` into the product repository. Start Claude Code from that repository and request one of the workflows described in `CLAUDE.md`.
