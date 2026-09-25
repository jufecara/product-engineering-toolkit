# Product Engineering Toolkit

An open-source, skills-first toolkit for helping product engineers understand, improve, ship, and learn from software products.

It is designed for new product engineers, project takeovers, long-running products with missing documentation, and systems that have gradually drifted away from a shared understanding of their purpose, rules, architecture, quality, or user experience.

## What product engineering means here

Product engineering is the practice of combining product context, customer understanding, design collaboration, software engineering, safe delivery, and measurement in one continuous loop. The goal is a useful product outcome—not merely completed tickets or deployed code.

The toolkit supports two complementary modes:

- **Practice:** frame a problem, shape a small slice, build safely, release, measure, and learn.
- **Assurance:** recover context and review architecture, security/privacy/reliability, quality, UX, and documentation.

Start with `product-engineering-practice` for a feature or ambiguous problem. Use `project-recovery` when the product context itself is missing, then route to the specialist reviews that match the risk.

![Product Engineering Toolkit](assets/product-engineering-toolkit-hero.png)

## What it does

The toolkit coordinates focused reviews that produce evidence-backed artifacts for both humans and coding agents:

- Product purpose, users, workflows, rules, and unknowns
- Repository and architecture understanding
- Architecture quality and technical-debt review
- Security, privacy, reliability, and operational readiness
- Test strategy, coverage, mutation, performance, and release confidence
- UI/UX heuristics, accessibility, and user friction
- Documentation completeness, freshness, and traceability
- Outcome framing, thin-slice shaping, release readiness, and post-release learning

It also includes a separate set of standalone, stack-agnostic hardening and hygiene checklists that
work independently of the review sequence above — CI/CD pipeline gating, code quality gates,
dependency management, PWA hardening, repository hygiene, security hardening, and testing
practices. Use any one of them in isolation for setup or review work.

The toolkit should be used selectively. Start with recovery when a project has lost important context. If the project is already well documented, use only the targeted review that the current change requires.

## Repository structure

```text
plugins/product-engineering-toolkit/
├── .codex-plugin/plugin.json   # Codex plugin manifest
├── skills/                     # Reusable specialist workflows
├── commands/                   # Optional explicit command entrypoints
├── references/                 # Shared collaboration rules
├── templates/                  # Reusable report templates
├── CLAUDE.md                   # Claude Code adapter
├── USAGE_GUIDE.md              # Workflow guide
└── README.md                   # Plugin-specific details
```

## Codex usage

Install or import the plugin according to your Codex environment, then use natural language or explicitly invoke a skill. The optional commands are convenience entrypoints, not a required process.

Recommended starting point for a feature or product problem:

```text
$product-engineering-practice
```

Recommended starting point for an unfamiliar or drifting project:

```text
$project-recovery
```

Or:

```text
Use project-recovery to assess whether this project has lost important context and propose the smallest useful recovery plan.
```

## Claude Code usage

Copy `plugins/product-engineering-toolkit/CLAUDE.md`, the relevant `skills/` files, and any needed `templates/` into the product repository. Start Claude Code from that repository and request a workflow explicitly.

## Evidence standard

Important claims must be labeled `confirmed`, `inferred`, `unknown`, or `needs validation`, with a source and confidence. A review identifies risks and validation actions; it does not automatically certify security, privacy, accessibility, compliance, reliability, or production readiness.

## Status

This is an early, skills-only release. It intentionally has no marketplace configuration, external service integration, or MCP server.

See [CONTRIBUTING.md](CONTRIBUTING.md) for adding skills and [plugins/product-engineering-toolkit/USAGE_GUIDE.md](plugins/product-engineering-toolkit/USAGE_GUIDE.md) for the complete workflow.
