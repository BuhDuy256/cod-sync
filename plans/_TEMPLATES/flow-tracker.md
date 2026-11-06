---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Flow tracker — {scope}

Local mirror of the GitHub flow tracker issue. Update this file when the issue is updated.

<!-- Document rules (WORKFLOW.md "Document rules"): front-load the "At a glance" block,
     keep the phase order below. Every #N must be a clickable link:
     [#N](https://github.com/{owner}/{repo}/issues/N) — see WORKFLOW.md "Linking convention". -->

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **Active phase:** Phase 1
- **Spine:** [traceability-matrix.md](./traceability-matrix.md)

## Phase 1: Research
<!-- Gate: all in-scope research tickets closed -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) question title

## Phase 2: Testing plan
<!-- Gate: all test stub tickets closed -->
<!-- Blocked by: Phase 1 complete -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) test stub title

## Phase 3: Implementation plan
<!-- Gate: plan reviewed and approved -->
<!-- Blocked by: Phase 2 complete -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) plan review

## Phase 4: Implementation
<!-- Gate: all impl tickets closed, tests green -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) module name (Blocked by: [#N](https://github.com/{owner}/{repo}/issues/N))

## Phase 5: Post-implementation testing
<!-- Gate: all post-impl tickets closed -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) test name (Blocked by: [#N](https://github.com/{owner}/{repo}/issues/N))

## Phase 6: Verification
<!-- Gate: flow tracker issue closed; every matrix row's Verified column is ticked -->
<!-- Blocked by: Phase 5 complete -->

- [ ] Full test suite passes
- [ ] Smoke tests pass

### Verified per AC
<!-- One line per AC, taken from plans/UC-XXX/traceability-matrix.md -->

- [ ] FR-NNN / AC-1 — confirmed on real code
- [ ] FR-NNN / AC-2 — confirmed on real code
