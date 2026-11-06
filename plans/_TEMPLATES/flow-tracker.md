---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Flow tracker — {scope}

Bản local của flow tracker issue trên GitHub. Cập nhật file này mỗi khi issue được cập nhật.

<!-- Document rules (WORKFLOW.md "Document rules"): đặt block "At a glance" lên đầu,
     giữ thứ tự phase bên dưới. Mọi #N phải là link bấm được:
     [#N](https://github.com/{owner}/{repo}/issues/N) — xem WORKFLOW.md "Linking convention". -->

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **Active phase:** Phase 1
- **Spine:** [traceability-matrix.md](./traceability-matrix.md)

## Phase 1: Research
<!-- Gate: mọi research ticket trong scope đã đóng -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) question title

## Phase 2: Testing plan
<!-- Gate: mọi test stub ticket đã đóng -->
<!-- Blocked by: Phase 1 complete -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) test stub title

## Phase 3: Implementation plan
<!-- Gate: plan đã được review và approve -->
<!-- Blocked by: Phase 2 complete -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) plan review

## Phase 4: Implementation
<!-- Gate: mọi impl ticket đã đóng, test xanh -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) module name (Blocked by: [#N](https://github.com/{owner}/{repo}/issues/N))

## Phase 5: Post-implementation testing
<!-- Gate: mọi post-impl ticket đã đóng -->

- [ ] [#N](https://github.com/{owner}/{repo}/issues/N) test name (Blocked by: [#N](https://github.com/{owner}/{repo}/issues/N))

## Phase 6: Verification
<!-- Gate: flow tracker issue đã đóng; cột Verified của mọi dòng trong matrix đã tick -->
<!-- Blocked by: Phase 5 complete -->

- [ ] Toàn bộ test suite pass
- [ ] Smoke test pass

### Verified per AC
<!-- Mỗi AC một dòng, lấy từ plans/UC-XXX/traceability-matrix.md -->

- [ ] FR-NNN / AC-1 — đã xác nhận trên code thật
- [ ] FR-NNN / AC-2 — đã xác nhận trên code thật
