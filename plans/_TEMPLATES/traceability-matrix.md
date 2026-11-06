---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Traceability matrix — {scope}

Spine truy vết của build. Mỗi FR/AC trong scope (và mỗi NFR) có một dòng, nối requirement → research/decision → test → implementation ticket → verification.

**No-orphan rule:** mỗi deliverable phải có nơi dùng nó ở phía sau. Không gate nào được đóng khi còn dòng thiếu link mà phase đó phải tạo ra (xem WORKFLOW.md "Traceability"). Matrix này là nơi duy nhất chứa spine. Các plan document khác link tới dòng của nó thay vì chép lại requirement (WORKFLOW.md "Document rules").

## At a glance

- **Use case:** UC-XXX
- **Steps:** S1-S2 (or "all")
- **Alternatives:** A1, A3 (or "all")
- **FRs in scope:** FR-NNN, FR-NNN
- **NFRs in scope:** NFR-NNN

<!-- Mọi #N và đường dẫn file là link bấm được (WORKFLOW.md "Linking convention"). -->

## Matrix

| FR / AC | RQ | DEC | Test (ticket) | Impl (ticket) | Verified |
|---|---|---|---|---|---|
| FR-NNN / AC-1 | [RQ-N](...) | [DEC-NNN](...) | [#N](https://github.com/{owner}/{repo}/issues/N) | [#N](https://github.com/{owner}/{repo}/issues/N) | [ ] |
| NFR-NNN | [RQ-N](...) | [DEC-NNN](...) | [#N](https://github.com/{owner}/{repo}/issues/N) | [#N](https://github.com/{owner}/{repo}/issues/N) | [ ] |

## Columns

- **FR / AC** — mỗi acceptance criterion trong scope một dòng. NFR không có AC thì dùng chính NFR làm dòng.
- **RQ** — research question đã trả lời cho dòng này (để trống nếu không cần).
- **DEC** — decision đã định hình dòng này (để trống nếu không có).
- **Test (ticket)** — acceptance/security test chứng minh AC. **Required:** mọi FR/AC và NFR trong scope có ít nhất một test.
- **Impl (ticket)** — implementation ticket làm cho dòng này pass.
- **Verified** — `[x]` khi Phase 6 đã xác nhận AC này trên code thật.

## Orphan check (run at every gate)

- [ ] Mọi FR/AC và NFR trong scope đều có dòng.
- [ ] Mọi dòng có ít nhất một Test ticket (sau Phase 2).
- [ ] Mọi DEC trong scope được ít nhất một dòng dùng tới (test hoặc impl).
- [ ] Mọi RQ đã trả lời dẫn tới một DEC hoặc một dòng dùng kết quả của nó.
- [ ] Không có Test/Impl ticket nào thiếu dòng trong matrix.
