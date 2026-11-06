# Plans

One subfolder per use case build. Each subfolder contains the workflow artifacts for that UC, created as the phases progress.

## Structure

```
plans/
├── _TEMPLATES/              Templates for plan documents
│   ├── research-checklist.md
│   ├── testing-plan.md
│   ├── implementation-plan.md
│   ├── traceability-matrix.md
│   └── flow-tracker.md
└── UC-XXX/                  One folder per UC build
    ├── research-checklist.md
    ├── testing-plan.md
    ├── implementation-plan.md
    ├── traceability-matrix.md  Spine: FR/AC → RQ/DEC → test → impl → verify
    └── flow-tracker.md      Local mirror of the GitHub Issue
```

## Lifecycle

- A UC folder is created at the start of Phase 1.
- The traceability matrix is seeded in Phase 1 and filled in as each phase produces its links (test, impl, verification). See WORKFLOW.md "Traceability".
- Files are added as each phase begins.
- The flow tracker is updated as tickets close.
- When the UC build is complete (Phase 6), all files remain as a record.
