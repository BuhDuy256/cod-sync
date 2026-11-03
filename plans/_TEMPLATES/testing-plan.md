---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Testing plan — {scope}

<!-- Document rules (WORKFLOW.md "Document rules"): front-load the "At a glance" block,
     reference matrix rows by FR/AC id (don't restate the requirement text), keep the
     section order below, keep under ~1 page. -->

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **NFRs in scope:** NFR-NNN
- **Status:** _N of N ACs mapped to a test_
- **Spine:** [traceability-matrix.md](./traceability-matrix.md) — every test here maps to a row there

## Test types

| Type | Purpose | When |
|---|---|---|
| Acceptance | Check an FR's acceptance criteria directly | Before implementation |
| Security | Check security-related ACs and the threat model | Before implementation |
| Unit | Check a single function / module in isolation | With implementation |
| Integration | Check modules working together | After implementation |
| E2E | Check the whole UC flow end to end | After implementation |
| Smoke | Minimal checks proving the build is not broken | After implementation |
| Recovery / resilience | Check behavior under failure | After implementation |
| Regression | Stop a fixed bug from returning | After implementation (ongoing) |
| Performance | Check an NFR's performance target | After implementation |

## Pre-implementation tests

### Acceptance tests

<!-- DEC column: the decision that shaped this test — so a changed decision points to the
     tests that must be revisited. Leave blank if none. -->

| AC | FR | DEC | Test description | Ticket | Status |
|---|---|---|---|---|---|
| AC-1 | FR-NNN | DEC-NNN | | #N | open |

### Security tests

| Threat / AC | FR | DEC | Test description | Ticket | Status |
|---|---|---|---|---|---|
| | FR-NNN | DEC-NNN | | #N | open |

## Tests with implementation (bundled into impl tickets)

| Module / function | FR | Test description | Impl ticket |
|---|---|---|---|
| | FR-NNN | | #N |

## Post-implementation tests

### E2E tests

| Flow | UC steps | Test description | Ticket | Status |
|---|---|---|---|---|
| Happy path | S1-S6 | | #N | open |

### Smoke tests

| Check | Description | Ticket | Status |
|---|---|---|---|
| | | #N | open |

### Recovery / resilience tests

| Failure scenario | UC alternative | Test description | Ticket | Status |
|---|---|---|---|---|
| | A-N | | #N | open |

### Performance tests

| Metric | NFR | Target | Test description | Ticket | Status |
|---|---|---|---|---|---|
| | NFR-NNN | | | #N | open |

### Regression tests

Added when a bug is found and fixed. Not planned ahead.
