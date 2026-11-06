---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Testing plan — {scope}

<!-- Document rules (WORKFLOW.md "Document rules"): đặt block "At a glance" lên đầu,
     nhắc tới dòng matrix bằng ID FR/AC (không chép lại nội dung requirement), giữ thứ tự
     section bên dưới, dài không quá ~1 trang. -->

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **NFRs in scope:** NFR-NNN
- **Status:** _N of N ACs mapped to a test_
- **Spine:** [traceability-matrix.md](./traceability-matrix.md) — mỗi test ở đây map tới một dòng ở đó

## Test types

| Type | Purpose | When |
|---|---|---|
| Acceptance | Kiểm tra trực tiếp acceptance criteria của một FR | Trước implementation |
| Security | Kiểm tra các AC liên quan tới bảo mật và threat model | Trước implementation |
| Unit | Kiểm tra riêng một function / module | Cùng lúc với implementation |
| Integration | Kiểm tra các module chạy cùng nhau | Sau implementation |
| E2E | Kiểm tra toàn bộ flow của UC từ đầu tới cuối | Sau implementation |
| Smoke | Kiểm tra tối thiểu để chứng minh build không bị hỏng | Sau implementation |
| Recovery / resilience | Kiểm tra hành vi khi có lỗi xảy ra | Sau implementation |
| Regression | Chặn một bug đã sửa quay lại | Sau implementation (liên tục) |
| Performance | Kiểm tra chỉ tiêu performance của một NFR | Sau implementation |

## Pre-implementation tests

### Acceptance tests

<!-- Cột DEC: decision đã định hình test này => khi decision đổi, biết ngay test nào
     phải xem lại. Để trống nếu không có. -->

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

Thêm vào khi tìm ra và sửa một bug. Không lên kế hoạch trước.
