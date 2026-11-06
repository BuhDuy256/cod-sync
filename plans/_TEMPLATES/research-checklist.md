---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Research checklist — {scope}

<!-- Document rules (WORKFLOW.md "Document rules"): đặt block "At a glance" lên đầu,
     link tới dòng matrix thay vì chép lại requirement, giữ thứ tự section bên dưới,
     dài không quá ~1 trang. Mọi #N và đường dẫn file là link bấm được (WORKFLOW.md
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

Mỗi câu hỏi gắn với FR/NFR mà nó phục vụ. Bảng options đi kèm chỉ liệt kê lựa chọn và tradeoff, không chứa câu trả lời. Câu trả lời nằm trong file deliverable, còn `Choice`/`Why` nằm trong decision record. Ai làm phần nào: xem WORKFLOW.md "Division of labor". File deliverable được tạo sẵn => mở file và điền vào các field còn trống.

## Flow model

<!-- Lần theo từng bước kỹ thuật xảy ra khi UC chạy. Mỗi bước ghi hệ thống làm gì lúc
     runtime. Research question được gắn vào bước mà nó phát sinh. -->

### {S1 — step name}

1. **S1.1** — {hành động kỹ thuật cụ thể}
2. **S1.2** — {hành động tiếp theo} → **RQ-N** _(chưa biết cách làm)_
3. **S1.3** — {hành động tiếp theo}

### {S2 — step name}

1. **S2.1** — {hành động kỹ thuật}
2. **S2.2** — {hành động} → **RQ-N** _(cần ra decision)_

### Alternative flows

#### {A1 — branch name} (tách ra từ S1.2)

1. **A1.1** — {xử lý lỗi / ngoại lệ} → **RQ-N** _(chưa biết cách xử lý)_

## Deliverable map

<!-- Link mỗi RQ tới file deliverable của nó. Dùng link Markdown đầy đủ. -->

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

- `open` — chưa bắt đầu
- `researching` — đang làm
- `answered` — đã trả lời trong docs/research/
- `decided` — đã quyết trong docs/decisions/DEC-NNN
