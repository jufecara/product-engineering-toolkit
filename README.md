# Product Engineering Toolkit

An open-source, skills-first toolkit for recovering lost product context and helping product engineers understand undocumented software systems.

It is designed for project takeovers, long-running products with missing documentation, and systems that have gradually drifted away from a shared understanding of their purpose, rules, architecture, quality, or user experience.

## What it does

The toolkit coordinates focused reviews that produce evidence-backed artifacts for both humans and coding agents:

- Product purpose, users, workflows, rules, and unknowns
- Repository and architecture understanding
- Architecture quality and technical-debt review
- Security, privacy, reliability, and operational readiness
- Test strategy, coverage, mutation, performance, and release confidence
- UI/UX heuristics, accessibility, and user friction
- Documentation completeness, freshness, and traceability

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

Recommended starting point:

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
