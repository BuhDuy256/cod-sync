---
scope: ""
title: ""
created: DD-MM-YYYY
status: draft
---

# Implementation plan — {scope}

<!-- Document rules (WORKFLOW.md "Document rules"): đặt block "At a glance" lên đầu,
     nhắc tới dòng matrix và test bằng ID (không chép lại nội dung), giữ thứ tự section
     bên dưới, dài không quá ~1 trang. -->

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **Decisions needed:** DEC-NNN, DEC-NNN
- **Status:** draft / reviewed / approved
- **Spine:** [traceability-matrix.md](./traceability-matrix.md) — mỗi step map tới một dòng ở đó

## Entry conditions

- [ ] Mọi research ticket trong scope đã đóng (gate Phase 1)
- [ ] Mọi test stub ticket trong scope đã đóng (gate Phase 2)

## Steps

### Step 1 — name

- **What to build:** module, function, đường dẫn file cần tạo hoặc sửa
- **Tests it makes pass:** #N (AC test), #N (unit test)
- **Depends on decision:** DEC-NNN
- **Depends on step:** none
- **Ticket:** #N

### Step 2 — name

- **What to build:**
- **Tests it makes pass:** #N
- **Depends on decision:** DEC-NNN
- **Depends on step:** Step 1
- **Ticket:** #N

## Dependency diagram

```mermaid
graph LR
  S1[Step 1] --> S2[Step 2]
  S2 --> S3[Step 3]
```

## Approval

- [ ] Reviewed
- [ ] Approved — chuyển sang tạo ticket
