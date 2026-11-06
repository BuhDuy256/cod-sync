---
id: NFR-000
title: ""
updated: YYYY-MM-DD
---

<!-- NFR là một ràng buộc chất lượng cấp product dưới một điều kiện đã nêu (NFG-01).
     Chỉ viết khi đủ cả bốn: một cam kết hay rủi ro của product cần nó; đo/kiểm tra được; thêm ràng buộc độc lập chứ không lặp lại FR; target có ý nghĩa với user (NFG-02).
     Không hành vi (đó là FR), không giá trị rule (đó là BR, cite [BR-xxx]), không metric engineering, không interface, không architecture, không tiến độ.
     File này không gọi tên use case, step, nhánh, FR hay NFR khác. File khác cite [NFR-xxx].
     Viết theo docs/spec/_STYLE.md. -->

## Requirement

<!-- Quality attribute: một thuộc tính, ví dụ performance, reliability, data integrity, security, privacy.
     Statement: chất lượng product phải giữ được, không kèm target.
     Status: confirmed | proposed. Why không bắt buộc, bỏ dòng khi không cần lý do. -->

- **Quality attribute:**
- **Statement:**
- **Status:** confirmed
- **Why:**

## Verification

<!-- Ít nhất một measure. Mỗi measure một block: "### M-n · name". ID không đánh số lại (NFG-08).
     Condition: trạng thái, input và môi trường, đủ để làm lại; nêu ranh giới product-controlled hay end-to-end; nêu điều kiện phụ thuộc provider, không giấu thời gian của provider.
     Measure: đại lượng được đo hoặc thuộc tính được kiểm tra. How to measure: đo/kiểm tra thế nào, viết bằng văn xuôi, không tool, không architecture.
     Target: một giá trị có đơn vị và giới hạn, hoặc một thuộc tính bắt buộc (kiểm tra bảo mật/riêng tư có thể là thuộc tính không phải số). "not set" khi chưa quyết; không đoán số.
     Passes when: thế nào là pass. "not set" khi chưa quyết. -->

### M-1 · measure name

- **Condition:**
- **Measure:**
- **How to measure:**
- **Target:** not set
- **Passes when:** not set

## Undecided

<!-- Khía cạnh còn mở mà không phải target, mỗi item một dòng, kết thúc bằng "Pending decision." (hoặc "Pending technical evidence." khi thiếu bằng chứng để định nghĩa).
     Target chưa quyết là "not set", không phải item ở đây. Bỏ section này nếu trống. -->

## Notes

<!-- Chỉ những gì không thuộc statement hay measure, ví dụ một lần tách hoặc gộp. Bỏ section này nếu trống. -->
