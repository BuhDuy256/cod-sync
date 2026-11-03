# Build workflow

Reference for building use cases from spec to working code. Every session that starts
a UC build reads this document.

## Trigger and scope

The workflow starts when the user requests a build. The scope is flexible:

| User says | Scope |
|---|---|
| "Build UC-001" | Full UC — all steps and alternatives |
| "Build the fetch flow from UC-001" | Steps S1-S2, alternatives A1-A3 |
| "Build just the link validation" | FR-001 only |
| "Build the error handling for fetch failure" | Alternative A3 only |
| "Build UC-001 S1-S3 without save" | Steps S1-S3, skip S6 and save-related alternatives |

The first action is always Phase 1, never jumping to implementation. The scope
determines which FRs/NFRs are included in research, testing, and implementation.

### Scope definition

Every build starts by defining its scope in the plan folder:

- **Folder name:** `plans/UC-XXX-short-label/` (e.g., `plans/UC-001-fetch-flow/`)
- **Scope fields** (in every plan template):
  - Use case: UC-XXX
  - Steps included: S1-S2 (or "all")
  - Alternatives included: A1, A3 (or "all")
  - FRs in scope: FR-001, FR-002
  - NFRs in scope: NFR-001

A full UC build uses `plans/UC-XXX/` with "all" for steps and alternatives.

### Multiple builds for the same UC

Different scopes of the same UC coexist:
- `plans/UC-001-fetch-flow/` — S1-S2
- `plans/UC-001-save-flow/` — S6 + A8, A11
- `plans/UC-001-audio-prep/` — S4-S5 + A6

Each has its own flow tracker issue and its own tickets.

## Resuming

When the user says "continue UC-XXX" (or a scoped build name), read the flow
tracker issue on GitHub first. It shows which phase is active and which tickets
are open.

## Division of labor

Every phase splits work between the user (the thinking that must stay with the
human) and the agent (the legwork). The agent proposes; nothing closes a gate until
the user has reviewed, given feedback, and approved. This split is deliberate: the
user keeps the research and the judgment so understanding of the system stays with
the person who owns it.

| Phase | User owns (research + judgment) | Agent owns (legwork) |
|---|---|---|
| 0 — Domain discovery | **Researches the domain and writes the notes. Picks the use cases.** | Generates the question checklist and points to public sources — does **not** answer the questions or propose the answer. |
| 1 — Research | **Researches and answers the questions. Writes the decision records** (`Choice` / `Why`). | Generates the question checklist and options/tradeoff tables as raw material — does **not** answer the questions or fill in the choice/rationale. |
| 2 — Testing plan | Reviews, gives feedback, approves. | Proposes the testing plan. |
| 3 — Implementation plan | Reviews, gives feedback, approves. | Proposes the ordered steps. |
| 4 — Tickets | Approves scope. | Writes the flash-ready tickets. |
| 5 — Execution | Reviews PRs, decides merges. | Implementers code; agent reviews. |
| 6 — Verification | **Judges against the acceptance criteria.** | Runs suites and reports results. |

This table governs — the `AGENTS.md` "Decision authority" lists say _who decides_;
this says _who does the work_.

## Traceability

Every build maintains one spine artifact: the **traceability matrix**
(`plans/UC-XXX/traceability-matrix.md`, from `plans/_TEMPLATES/`). One row per FR/AC
(and per NFR), threading `FR/AC → RQ/DEC → test → impl ticket → verification`.

**No-orphan rule:** every deliverable must have a named consumer downstream. A
deliverable that nothing later uses is a defect, not neutral. Concretely:

- Every in-scope FR/AC and NFR has a matrix row.
- Every in-scope FR/AC and NFR has at least one test (after Phase 2).
- Every decision (DEC) is consumed by at least one test or implementation step.
- Every answered research question (RQ) leads to a DEC or a row that uses its result.
- Every test and implementation ticket maps back to a matrix row.

The matrix is seeded in Phase 1 (rows for every in-scope FR/AC/NFR) and filled in as
each phase produces its links. **No phase gate closes while the matrix has an orphan
that phase was responsible for resolving** — this clause is added to every gate below.

## Document rules

Every generated plan document (and the templates in `plans/_TEMPLATES/`) follows five
rules. Rule 5 applies to every document in the repository. They serve two readers at once: a person skimming the file, and an agent that
re-reads it each phase and pays tokens for every line. The rules are the same because
the fix is the same — front-load the essential, and never say a thing twice.

1. **Front-load.** The file opens with an `## At a glance` block: the scope, the
   current status, and a link to the one artifact that matters (usually the matrix).
   That block is the whole summary — nothing below it is required reading. A person
   reads it and stops; an agent reads it and only dives deeper if the task needs it.
2. **Link, don't restate.** One fact lives in one home. A testing plan, an
   implementation plan, or the flow tracker references a matrix row (by FR/AC id and
   link) — it never copies the requirement text. Duplication is the biggest token
   waste and the biggest readability drag (the reader can't tell which copy is
   authoritative). The matrix is the home for the FR/AC → test → impl spine.
3. **Fixed section order.** Each template fixes its heading order and the generator
   keeps it. Predictable anchors let a reader (human or agent) jump to just one
   section — a gate, a table — instead of reading the whole file.
4. **Length budget.** Keep each document under about one page. If it grows past that,
   split it or link out rather than inline more. The budget is what forces rule 2.
5. **State content, not provenance.** A document says what it holds and what it is
   for. It does not say who wrote it, who answers it, or who decides. Roles live only
   in "Division of labor"; link there when a reader needs them. Git records authorship.

## Phases

### Phase 0 — Domain discovery

**Goal:** understand the domain well enough to choose use cases for a reason, not by
guess. Runs once per product (and again when a new area of the domain opens), before
any UC build. It is upstream of the build phases: Phase 1 answers technical unknowns
for a use case that already exists; Phase 0 decides which use cases should exist.

**Input:** the brief (`docs/spec/00-brief/`) and the vision (`docs/spec/01-product-vision/`).

**Process:**

1. The agent keeps the domain checklist at `docs/research/domain/README.md` (areas, the
   spec item each area unlocks, sources to start from) and opens one GitHub Issue per
   area, label `phase:domain`. The issue holds the area's numbered questions as a task
   list; the questions live only there.
2. **The user researches and writes one note per area** in `docs/research/domain/`,
   following `docs/research/_STYLE.md` (problem → what was tried → what was observed →
   what it means). A question is closed by answering it in the note, or by marking it
   out of scope with a one-line reason, then ticking it in the issue. The area's Status
   in the checklist is updated, and the issue is closed when every question is ticked.
3. Each finished note feeds the spec: a glossary row in `docs/spec/_STYLE.md`, a
   business-rule value, a discrepancy type with its source, stronger `Evidence` on a
   vision `W-x` block, or a use case candidate. Who decides: `AGENTS.md` "Decision
   authority".
4. The user picks the use cases and the first build from the notes. Each use case links
   the note it came from in its `Product evidence` section.

**Gate:** the user explains the COD cash flow and the discrepancy catalog in their own
words; every checklist question is answered or marked out of scope; every chosen use
case links at least one domain note (no use case without a reason).

### Phase 1 — Research

**Goal:** answer every technical unknown before planning.

**Input:** the UC file, its FRs, NFRs, BRs.

**Process:**

1. Run skill `research-questions` on the UC to generate a research checklist.
2. Create the checklist at `plans/UC-XXX/research-checklist.md`.
3. Seed the traceability matrix at `plans/UC-XXX/traceability-matrix.md` from
   `plans/_TEMPLATES/traceability-matrix.md` — one row per in-scope FR/AC and NFR.
4. Create GitHub Issues for each question using the `research-ticket` template.
   Label: `phase:research`, `uc:XXX`.
5. The agent provides options with a tradeoffs table for technical questions — as
   raw material only. It does not answer the questions.
6. **The user researches and writes the answer.** Each answered question produces
   either:
   - An update to the research file in `docs/research/`, or
   - A decision record in `docs/decisions/DEC-NNN-topic.md` — the user fills in the
     `Choice` and `Why` in their own words.
7. Close each research ticket when its question is answered or decided, and record
   the RQ/DEC link on the matrix row(s) it serves.

**Gate:** all research tickets for this UC are closed; the matrix is seeded with a
row per in-scope FR/AC/NFR; every answered RQ leads to a DEC or a row that uses its
result (no orphan research).

### Phase 2 — Testing plan

**Goal:** define every test before writing any implementation.

**Input:** FRs with ACs, NFRs, decisions from Phase 1.

**Process:**

1. Run skill `testing-plan` on the UC's FRs/ACs and decisions.
2. Create the plan at `plans/UC-XXX/testing-plan.md`.
3. Create GitHub Issues for pre-implementation test stubs using the `test-stub-ticket`
   template. Label: `phase:test-stubs`, `uc:XXX`.
4. Test types and their phases:

   | Type | When written | Phase label |
   |---|---|---|
   | Acceptance tests | Before implementation | `phase:test-stubs` |
   | Security tests | Before implementation | `phase:test-stubs` |
   | Unit tests | Bundled into implementation tickets | `phase:impl` |
   | Integration tests | After the modules they test | `phase:post-impl` |
   | E2E tests | After all implementation | `phase:post-impl` |
   | Smoke tests | After all implementation | `phase:post-impl` |
   | Recovery / resilience tests | After the modules they test | `phase:post-impl` |
   | Regression tests | Grows over time with bug fixes | `phase:post-impl` |
   | Performance tests | After implementation, when NFRs exist | `phase:post-impl` |

5. Close each test stub ticket when the test file exists and the stub runs (red).
6. Record each test ticket on its matrix row, and note the DEC each test depends on.

**Gate:** all `phase:test-stubs` tickets for this UC are closed; every matrix row
has at least one test; every in-scope DEC is consumed by at least one test (no
untested requirement, no orphan decision).

### Phase 3 — Implementation plan

**Goal:** produce an ordered list of implementation steps tied to tests.

**Input:** testing plan, decisions, research answers.

**Process:**

1. Create the plan at `plans/UC-XXX/implementation-plan.md`.
2. Each step references:
   - What to build (module, function, file path).
   - Which tests it makes pass.
   - Which decisions it depends on.
3. The user reviews and approves the plan.

**Gate:** user approves the implementation plan; every matrix row has at least one
implementation step (no requirement left unbuilt).

### Phase 4 — Implementation tickets

**Goal:** break the plan into flash-model-friendly GitHub Issues.

**Input:** approved implementation plan.

**Process:**

1. Create GitHub Issues using the `implementation-ticket` template.
   Label: `phase:impl`, `uc:XXX`.
2. Each ticket has:
   - `Blocked by` referencing its prerequisite tickets (test stubs, other modules).
   - A test command as acceptance criteria.
   - Explicit `Do NOT` boundaries.
3. Create post-implementation test tickets using the `post-impl-test-ticket` template.
   Label: `phase:post-impl`, `uc:XXX`.
   These are blocked by the implementation tickets they depend on.
4. Update the flow tracker issue with all ticket numbers.
5. Fill the matrix Test and Impl columns with the ticket links.

**Gate:** all tickets created and linked; the matrix Test/Impl columns are filled;
no test or implementation ticket exists without a matrix row (no orphan ticket).

### Phase 5 — Execution and review

**Goal:** implement all tickets and pass all tests.

**Input:** tickets in dependency order.

**Process:**

1. The user assigns tickets to implementers (DeepSeek/GLM Flash via external tools,
   or Claude sub-agents).
2. Each implementer:
   - Reads the ticket and its linked context.
   - Pushes a branch with the implementation.
   - Runs the test command in the ticket to self-verify.
3. Claude reviews each PR using `/code-review`.
4. Merge when tests pass and review approves.
5. Close the ticket.
6. Update the flow tracker issue.

**Gate:** all `phase:impl` and `phase:post-impl` tickets are closed.

### Phase 6 — Verification

**Goal:** confirm the UC works end-to-end.

**Input:** all code merged, all tests green.

**Process:**

1. Run the full test suite.
2. Run smoke tests.
3. Run E2E tests for the UC's happy path and alternative flows.
4. Run resilience tests for the UC's failure alternatives.
5. Verify against the UC's acceptance criteria **row by row on the matrix** — tick
   the Verified column for each AC confirmed on the real code. The user makes this
   judgment (see "Division of labor").
6. Close the flow tracker issue.

**Gate:** flow tracker issue closed; every matrix row's Verified column is ticked
(every AC verified end-to-end). UC is done.

## Flow tracker issue

Every scoped build has one flow tracker issue — the root issue. It is created at the
start of Phase 1 and links to every other ticket. The scope definition appears at the
top. Template: `.github/ISSUE_TEMPLATE/flow-tracker.md`.

The tracker uses the format (local files use full links per "Linking convention";
GitHub issue bodies use bare `#N` which auto-links):

```markdown
## Phase 1: Research
- [ ] [#N]({base}/issues/N) question-title (status)

## Phase 2: Testing Plan
- [ ] [#N]({base}/issues/N) test-stub-title
Blocked by: Phase 1 complete

## Phase 3: Implementation Plan
- [ ] [#N]({base}/issues/N) plan-review
Blocked by: Phase 2 complete

## Phase 4: Implementation
- [ ] [#N]({base}/issues/N) module-title
Blocked by: [#test-stub]({base}/issues/N), [#other-module]({base}/issues/N)

## Phase 5: Post-impl Testing
- [ ] [#N]({base}/issues/N) test-title
Blocked by: [#module]({base}/issues/N)

## Phase 6: Verification
Blocked by: Phase 5 complete
```

## Ticket rules for flash models

Flash models (DeepSeek V4.1 Flash, GLM 5.3 Flash) need tickets with minimal reasoning
steps. Every implementation ticket must follow these rules:

1. **One concern per ticket.** One function, one component, one module.
2. **Exact file paths.** Not "create a validation module" but "create
   `src/domain/source-validator.ts`".
3. **Input/output contract.** Function signature, parameter types, return type.
4. **Test command.** The command that proves the ticket is done.
5. **Do NOT section.** Explicit boundaries — what NOT to touch, refactor, or change.
6. **Blocked by.** Prerequisites must be merged before starting.
7. **Context section.** What already exists that the implementer needs to know. Include
   file paths and brief descriptions, not "see the codebase".
8. **Maximum 3 files changed per ticket.** If more files need changing, split the ticket.

## Labels

| Label | Meaning |
|---|---|
| `uc:XXX` | Which use case this ticket belongs to |
| `phase:research` | Phase 1 ticket |
| `phase:test-stubs` | Phase 2 ticket |
| `phase:impl-plan` | Phase 3 ticket |
| `phase:impl` | Phase 4 implementation ticket |
| `phase:post-impl` | Phase 5 post-implementation test ticket |
| `flow-tracker` | The root tracker issue for a UC |
| `flash-ready` | Ticket is suitable for a flash model implementer |

## Milestones

One milestone per UC build: `UC-XXX`. All tickets for that UC belong to it.

## Linking convention

Every cross-reference between files, issues and deliverables must be a clickable
Markdown link — never a bare `#N` or a plain file path. This applies to all outputs:
plan files, issue bodies, research files, decision files, and flow tracker updates.

Derive the repo base URL from `git remote get-url origin` at the start of each build.

| Reference type | Format |
|---|---|
| Issue from a local file | `[#N](https://github.com/{owner}/{repo}/issues/N)` |
| File from an issue body | `[docs/research/topic.md](https://github.com/{owner}/{repo}/blob/main/docs/research/topic.md)` |
| Issue from an issue body | `#N` (GitHub auto-links these; no change needed) |
| Blocked-by in a local file | `[#N](https://github.com/{owner}/{repo}/issues/N)` |

**Where to apply:**

- **Research checklist** — Ticket column, Deliverable map File column
- **Flow tracker** (local `plans/` mirror) — all `#N` references
- **Research files** (`docs/research/`) — `**Ticket:**` and `**Blocked by:**` fields
- **Decision files** (`docs/decisions/`) — `ticket #N` references
- **Issue bodies** — Deliverable section (link to file), Flow tracker reference (auto-linked)
