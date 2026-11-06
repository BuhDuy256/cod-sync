# Plans

Mỗi build của một use case có một subfolder. Mỗi subfolder chứa các artifact của workflow cho UC đó, được tạo dần theo từng phase.

## Structure

```
plans/
├── _TEMPLATES/              Template cho các plan document
│   ├── research-checklist.md
│   ├── testing-plan.md
│   ├── implementation-plan.md
│   ├── traceability-matrix.md
│   └── flow-tracker.md
└── UC-XXX/                  Mỗi UC build một folder
    ├── research-checklist.md
    ├── testing-plan.md
    ├── implementation-plan.md
    ├── traceability-matrix.md  Spine: FR/AC → RQ/DEC → test → impl → verify
    └── flow-tracker.md      Bản local của GitHub Issue
```

## Lifecycle

- Folder của UC được tạo khi bắt đầu Phase 1.
- Traceability matrix được tạo sẵn các dòng ở Phase 1, rồi điền dần khi mỗi phase tạo ra link của nó (test, impl, verification). Xem WORKFLOW.md "Traceability".
- File được thêm vào khi mỗi phase bắt đầu.
- Flow tracker được cập nhật khi ticket đóng.
- Khi UC build hoàn tất (Phase 6), mọi file được giữ lại làm hồ sơ.
