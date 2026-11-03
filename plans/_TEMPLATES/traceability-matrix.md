---
scope: ""
title: ""
created: DD-MM-YYYY
---

# Ma trận truy vết — {scope}

Xương sống truy vết của lần build. Một dòng cho mỗi FR/AC trong phạm vi, lần theo
từ yêu cầu → nghiên cứu/quyết định → test → ticket implementation → xác nhận.

**Quy tắc không mồ côi (no-orphan):** mỗi deliverable phải có người tiêu thụ ở
bước sau. Không được đóng gate của một phase nếu còn dòng thiếu mắt xích mà phase
đó phải tạo ra (xem WORKFLOW.md "Truy vết").

## Phạm vi

- **Use case:** UC-XXX
- **Các bước:** S1-S2 (hoặc "tất cả")
- **Nhánh thay thế:** A1, A3 (hoặc "tất cả")
- **FR liên quan:** FR-NNN, FR-NNN
- **NFR liên quan:** NFR-NNN

<!-- Mọi tham chiếu #N và đường dẫn file phải là link clickable.
     Xem WORKFLOW.md "Linking convention". -->

## Ma trận

| FR / AC | RQ | DEC | Test (ticket) | Impl (ticket) | Xác nhận |
|---|---|---|---|---|---|
| FR-NNN / AC-1 | [RQ-N](...) | [DEC-NNN](...) | [#N](https://github.com/{owner}/{repo}/issues/N) | [#N](https://github.com/{owner}/{repo}/issues/N) | [ ] |
| NFR-NNN | [RQ-N](...) | [DEC-NNN](...) | [#N](https://github.com/{owner}/{repo}/issues/N) | [#N](https://github.com/{owner}/{repo}/issues/N) | [ ] |

## Cột

- **FR / AC** — mỗi điều kiện chấp nhận trong phạm vi là một dòng. NFR không có AC
  thì dùng chính NFR làm dòng.
- **RQ** — câu hỏi nghiên cứu đã trả lời cho dòng này (có thể trống nếu không cần).
- **DEC** — quyết định định hình dòng này (có thể trống nếu không có).
- **Test (ticket)** — acceptance/security test chứng minh AC. **Bắt buộc** mỗi FR/AC
  và mỗi NFR trong phạm vi có ít nhất một test.
- **Impl (ticket)** — ticket implementation làm dòng này pass.
- **Xác nhận** — `[x]` khi Phase 6 đã xác nhận AC này đạt trên code thật.

## Kiểm tra mồ côi (chạy ở mỗi gate)

- [ ] Mọi FR/AC và NFR trong phạm vi có một dòng.
- [ ] Mọi dòng có ít nhất một Test ticket (sau Phase 2).
- [ ] Mọi DEC trong phạm vi được tiêu thụ bởi ít nhất một dòng (test hoặc impl).
- [ ] Mọi RQ đã trả lời dẫn tới một DEC hoặc một dòng dùng kết quả đó.
- [ ] Không có Test/Impl ticket nào không gắn với một dòng.
