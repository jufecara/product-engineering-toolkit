---
name: testing-practices
description: "Testing conventions for any codebase: test co-location, deterministic time handling, shared test setup/helpers, and coverage reporting. Use when setting up a test suite from scratch, or reviewing an existing suite for flakiness, duplication, or missing coverage tooling."
risk: safe
source: personal
date_added: "2026-09-13"
---

# Testing Practices

> Stack-agnostic — applies regardless of test runner (Vitest, Jest, pytest, RSpec, go test, etc.).

## 1. Co-locate tests with source

- Place a unit test next to the file it tests (`module.ts` + `module.test.ts`), not in a mirrored
  `__tests__/` or `test/` tree. It keeps a moved/renamed file's test visibly attached, and makes
  "does this have a test?" answerable at a glance.
- Reserve a top-level test directory only for cross-cutting setup, shared helpers, and true
  integration/e2e tests that don't belong to one module.

## 2. Deterministic time and randomness

- Never let a test depend on real wall-clock waiting (`setTimeout` + real delay). Use the test
  framework's fake-timer facility (`vi.useFakeTimers()`, `jest.useFakeTimers()`, `freezegun`,
  etc.) and advance time programmatically. This makes time-based tests both fast and reliable.
- Reset fake timers/mocks in `afterEach` so state never leaks between tests.
- Seed or mock any randomness a unit under test relies on, so failures are reproducible.

## 3. Shared setup, not copy-paste

- Centralize test environment setup (global mocks, polyfills, DOM environment config) in one
  setup file wired into the test runner config, rather than repeating boilerplate per file.
- Extract shared rendering/bootstrapping helpers (e.g. a custom `render` that wraps providers)
  into a `test-utils` module so provider wiring changes happen in one place.

## 4. Coverage as a signal, not a vanity metric

- Configure coverage reporting (text summary for local/CI logs, HTML for local browsing, lcov
  for external tooling) and exclude test files, config files, and generated code from the
  denominator — otherwise the percentage is meaningless.
- Don't chase 100% coverage as a goal in itself; use coverage gaps to find *untested logic
  paths*, especially branches in business-critical code.

## 5. Test logic before wiring it into UI/integration

- For business-logic-heavy modules (parsers, generators, validators, calculators, state
  machines), write focused unit tests against the pure logic first, before or immediately after
  wiring it into a component/handler/controller. Logic bugs are far cheaper to isolate and fix
  in a unit test than through an integration or UI test.

## Verification checklist

- [ ] Tests live next to the source files they cover.
- [ ] No test relies on real elapsed time; fake timers/clocks are used and reset per test.
- [ ] A single setup file and shared test helpers exist instead of duplicated boilerplate.
- [ ] Coverage reporting is configured and excludes non-source files.
- [ ] Core business logic has direct unit tests, not just indirect coverage via UI tests.
