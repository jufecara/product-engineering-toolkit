---
name: code-quality-gates
description: "Enforced (not optional) code quality practices for any language: formatter + linter with zero-warning tolerance, pre-commit hooks scoped to staged files, and layered lint config. Use when setting up a new project's quality tooling, or hardening an existing project where lint/format issues accumulate unchecked."
risk: safe
source: personal
date_added: "2026-09-13"
---

# Code Quality Gates

> Stack-agnostic. Substitute the tool names for the target ecosystem
> (ESLint/Prettier for JS-TS, ruff/black for Python, gofmt/golangci-lint for Go,
> rustfmt/clippy for Rust, rubocop for Ruby, etc.) — the practice matters, not the tool.

## 1. One formatter, enforced

- Pick a single opinionated formatter for the language and commit its config file so every
  contributor and CI produce identical output.
- Provide two scripts: one that rewrites files (`format`) and one that only checks and exits
  non-zero on drift (`format:check`). CI must run the check variant, never the write variant.
- Also format non-code files that benefit from it (JSON, Markdown, YAML, CSS) if the formatter
  supports them.

## 2. One linter, zero tolerance

- Enable the linter's strictest "fail on any warning" mode (e.g. ESLint `--max-warnings=0`,
  `ruff check --exit-non-zero-on-fix`). A codebase that tolerates warnings accumulates them
  forever — nobody fixes a pre-existing warning while shipping a feature.
- Layer the lint config: base recommended rules → framework/ecosystem plugin rules → a
  formatter-compatibility layer that disables any lint rule that fights with the formatter
  (don't let two tools disagree about the same line).
- Promote high-value framework-specific rules from "warn" to "error" explicitly when the default
  is too lax (e.g. React's `exhaustive-deps` rule, a null-safety rule, an unused-import rule).
- Exclude generated/build/vendored directories from lint globs explicitly.

## 3. Pre-commit hooks scoped to staged files

- Use a git-hooks manager (Husky, pre-commit, lefthook, etc.) with automatic installation on
  dependency install (e.g. an `npm prepare` script, or a documented one-time setup step) so
  hooks aren't something contributors have to remember to enable.
- Run a staged-files-only tool (lint-staged or equivalent) so the hook only touches what's being
  committed, not the whole repo — keeps it fast (seconds, not minutes).
- Order pre-commit steps: fastest/highest-signal first (e.g. a quick security audit), then
  lint+format on staged files. Leave the full test suite and full build out of pre-commit —
  those belong in CI, otherwise contributors start using `--no-verify` out of frustration.

## 4. Type checking (if the language supports it)

- Run the type checker as its own explicit step, separate from linting and from the build
  (`tsc --noEmit`, `mypy`, etc.) so a type error is diagnosed clearly rather than buried in a
  bundler error.
- Enable strict-mode flags deliberately (unused locals/params, no-fallthrough, strict null
  checks) rather than accepting the loose default.

## Verification checklist

- [ ] `format:check` and `lint` (zero-warning) both exist as scripts and both run in CI.
- [ ] Formatter and linter configs don't fight each other (compatibility layer in place).
- [ ] Pre-commit hook installs automatically and only touches staged files.
- [ ] Full test suite and build are NOT in the pre-commit hook (only in CI).
- [ ] Type checker (if applicable) runs as a distinct, separate step.
