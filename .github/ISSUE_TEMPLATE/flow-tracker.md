---
name: Flow tracker
about: Issue gốc theo dõi một build scope. Mỗi build có scope một issue.
title: "Flow tracker — "
labels: flow-tracker
---

## Scope

- **Use case:** UC-XXX
- **Steps:** (ví dụ S1-S2, hoặc "all")
- **Alternatives:** (ví dụ A1, A3, hoặc "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **NFRs in scope:** NFR-NNN
- **Plans:** plans/UC-XXX-short-label/

## Phase 1: Research
<!-- Gate: mọi research ticket trong scope đã đóng -->

_Ticket được thêm vào khi tạo checklist research question._

## Phase 2: Testing plan
<!-- Gate: mọi test stub ticket đã đóng -->
<!-- Blocked by: Phase 1 complete -->

_Ticket được thêm vào khi tạo testing plan._

## Phase 3: Implementation plan
<!-- Gate: plan đã được review và approve -->
<!-- Blocked by: Phase 2 complete -->

- [ ] Implementation plan đã được review và approve

## Phase 4: Implementation
<!-- Gate: mọi impl ticket đã đóng, test xanh -->

_Ticket được thêm vào khi implementation plan được approve._

## Phase 5: Post-implementation testing
<!-- Gate: mọi post-impl ticket đã đóng -->

_Ticket được thêm vào cùng lúc với implementation ticket._

## Phase 6: Verification
<!-- Gate: issue này đã đóng; cột Verified của mọi dòng matrix đã tick -->
<!-- Blocked by: Phase 5 complete -->

- [ ] Toàn bộ test suite pass
- [ ] Smoke test pass

### Verified per AC
<!-- Mỗi AC một dòng, lấy từ plans/UC-XXX/traceability-matrix.md -->

_Danh sách AC được thêm từ traceability matrix khi tới Phase 6._
