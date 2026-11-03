---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Research checklist — {scope}

<!-- Document rules (WORKFLOW.md "Document rules"): front-load the "At a glance" block,
     link to matrix rows instead of restating requirements, keep the section order below,
     keep under ~1 page. Every #N and file path is a clickable link (WORKFLOW.md
     "Linking convention"). -->

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **NFRs in scope:** NFR-NNN
- **Status:** _N open / N answered / N decided_
- **Spine:** [traceability-matrix.md](./traceability-matrix.md)

## How to use

Each question is tied to the FR/NFR it serves. **The user researches and answers** —
the agent supplies only the questions and the options tables as raw material. The agent
does not answer for the user and does not fill in `Choice`/`Why` of a decision record
(see WORKFLOW.md "Division of labor"). The deliverable files are created ahead of time —
open the file and fill the empty fields.

## Flow model

<!-- Trace each technical step that happens when the UC runs. Each step shows what the
     system does at runtime. A research question is pinned to the step it arises from. -->

### {S1 — step name}

1. **S1.1** — {specific technical action}
2. **S1.2** — {next action} → **RQ-N** _(don't know how)_
3. **S1.3** — {next action}

### {S2 — step name}

1. **S2.1** — {technical action}
2. **S2.2** — {action} → **RQ-N** _(decision needed)_

### Alternative flows

#### {A1 — branch name} (splits from S1.2)

1. **A1.1** — {error / exception handling} → **RQ-N** _(don't know how to handle)_

## Deliverable map

<!-- Link each RQ to its deliverable file. Use full Markdown links. -->

| RQ | Type | File |
|---|---|---|
| RQ-1 | research | [docs/research/topic.md](https://github.com/{owner}/{repo}/blob/main/docs/research/topic.md) |

## Questions

### FR-NNN — name

| # | Question | Why it matters | Ticket | Status |
|---|---|---|---|---|
| RQ-1 | | | [#N](https://github.com/{owner}/{repo}/issues/N) | open |

### NFR-NNN — name

| # | Question | Why it matters | Ticket | Status |
|---|---|---|---|---|
| RQ-N | | | [#N](https://github.com/{owner}/{repo}/issues/N) | open |

## Status values

- `open` — not started
- `researching` — in progress
- `answered` — answered in docs/research/
- `decided` — decided in docs/decisions/DEC-NNN
