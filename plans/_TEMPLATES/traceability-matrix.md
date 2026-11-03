---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Traceability matrix — {scope}

The build's traceability spine. One row per in-scope FR/AC (and per NFR), threading
requirement → research/decision → test → implementation ticket → verification.

**No-orphan rule:** every deliverable must have a consumer downstream. No phase gate
closes while a row is missing a link that phase was responsible for producing (see
WORKFLOW.md "Traceability"). This matrix is the home for the spine — other plan
documents link to its rows instead of restating requirements (WORKFLOW.md "Document
rules").

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **NFRs in scope:** NFR-NNN

<!-- Every #N and file path is a clickable link (WORKFLOW.md "Linking convention"). -->

## Matrix

| FR / AC | RQ | DEC | Test (ticket) | Impl (ticket) | Verified |
|---|---|---|---|---|---|
| FR-NNN / AC-1 | [RQ-N](...) | [DEC-NNN](...) | [#N](https://github.com/{owner}/{repo}/issues/N) | [#N](https://github.com/{owner}/{repo}/issues/N) | [ ] |
| NFR-NNN | [RQ-N](...) | [DEC-NNN](...) | [#N](https://github.com/{owner}/{repo}/issues/N) | [#N](https://github.com/{owner}/{repo}/issues/N) | [ ] |

## Columns

- **FR / AC** — one row per in-scope acceptance criterion. An NFR with no AC uses the
  NFR itself as the row.
- **RQ** — the answered research question for this row (may be empty if none was needed).
- **DEC** — the decision that shaped this row (may be empty if none).
- **Test (ticket)** — the acceptance/security test that proves the AC. **Required:** every
  in-scope FR/AC and every NFR has at least one test.
- **Impl (ticket)** — the implementation ticket that makes this row pass.
- **Verified** — `[x]` once Phase 6 has confirmed this AC on the real code.

## Orphan check (run at every gate)

- [ ] Every in-scope FR/AC and NFR has a row.
- [ ] Every row has at least one Test ticket (after Phase 2).
- [ ] Every in-scope DEC is consumed by at least one row (test or impl).
- [ ] Every answered RQ leads to a DEC or a row that uses its result.
- [ ] No Test/Impl ticket exists without a matrix row.
