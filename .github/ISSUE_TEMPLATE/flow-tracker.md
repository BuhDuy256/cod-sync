---
name: Flow tracker
about: Root tracking issue for a build scope. One per scoped build.
title: "Flow tracker — "
labels: flow-tracker
---

## Scope

- **Use case:** UC-XXX
- **Steps:** (e.g. S1-S2, or "all")
- **Alternatives:** (e.g. A1, A3, or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **NFRs in scope:** NFR-NNN
- **Plans:** plans/UC-XXX-short-label/

## Phase 1: Research
<!-- Gate: all in-scope research tickets closed -->

_Tickets added when the research question checklist is created._

## Phase 2: Testing plan
<!-- Gate: all test stub tickets closed -->
<!-- Blocked by: Phase 1 complete -->

_Tickets added when the testing plan is created._

## Phase 3: Implementation plan
<!-- Gate: plan reviewed and approved -->
<!-- Blocked by: Phase 2 complete -->

- [ ] Implementation plan reviewed and approved

## Phase 4: Implementation
<!-- Gate: all impl tickets closed, tests green -->

_Tickets added when the implementation plan is approved._

## Phase 5: Post-implementation testing
<!-- Gate: all post-impl tickets closed -->

_Tickets added alongside the implementation tickets._

## Phase 6: Verification
<!-- Gate: this issue closed; every matrix row's Verified column is ticked -->
<!-- Blocked by: Phase 5 complete -->

- [ ] Full test suite passes
- [ ] Smoke tests pass

### Verified per AC
<!-- One line per AC, taken from plans/UC-XXX/traceability-matrix.md -->

_AC list added from the traceability matrix when Phase 6 is reached._
