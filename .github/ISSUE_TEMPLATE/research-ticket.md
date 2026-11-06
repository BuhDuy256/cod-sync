---
name: Research ticket
about: Một câu hỏi kỹ thuật hoặc sản phẩm cần trả lời trước implementation.
title: "Research: "
labels: phase:research
---

## Context

**Use case:** UC-XXX
**Related FR/NFR:** FR-NNN / NFR-NNN
**Flow step:** S?.? — {step name}
**Flow tracker:** #N

## Flow diagram

<!-- Mermaid sequence diagram thể hiện runtime flow của UC.
     Highlight (các) step mà câu hỏi này liên quan bằng `activate` / `note`.
     Người đọc cần thấy câu hỏi phát sinh từ CHỖ NÀO trong flow
     trước khi đọc câu hỏi. -->

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant Backend
    participant External

    User->>Frontend: action
    Frontend->>Backend: request

    rect rgb(255, 230, 150)
        note right of Backend: 👉 RQ-N: this step
        Backend->>External: operation
        External-->>Backend: response
    end

    Backend-->>Frontend: result
    Frontend-->>User: feedback
```

<!-- Thay diagram trên bằng flow thật của UC.
     Dùng `rect rgb(255, 230, 150)` để highlight (các) step
     mà research question này phát sinh. -->

## Question

<!-- Câu hỏi cụ thể cần trả lời. Mỗi ticket một câu hỏi. -->

## Why this matters

<!-- Requirement hoặc decision nào phụ thuộc vào câu trả lời này. Ghi cụ thể. -->

## Options (if technical)

<!-- Điền bảng khi câu hỏi là lựa chọn công nghệ. Xóa nếu không áp dụng. -->

| Option | Description | Fits requirements | Tradeoffs |
|---|---|---|---|
| Option A | | | |
| Option B | | | |
| Option C | | | |

## Deliverable

<!-- Đóng ticket này tạo ra gì. Dùng link bấm được để reviewer
     mở file trực tiếp. Format:

     **Decision record:** [docs/decisions/DEC-NNN-topic.md](https://github.com/BuhDuy256/cod-sync/blob/main/docs/decisions/DEC-NNN-topic.md)

     **Research answer:** [docs/research/topic.md](https://github.com/BuhDuy256/cod-sync/blob/main/docs/research/topic.md), section RQ-N -->

## Acceptance

- [ ] Câu hỏi đã được trả lời kèm bằng chứng hoặc lập luận
- [ ] File deliverable đã được tạo hoặc cập nhật
- [ ] Đã review

## Blocked by

<!-- Liệt kê ticket tiên quyết. Xóa nếu không có. -->
