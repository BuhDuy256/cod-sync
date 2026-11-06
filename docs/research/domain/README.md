# Domain discovery checklist

Các mảng cần research trước khi chọn use case. Mỗi mảng có một note trong folder này và một ticket chứa các câu hỏi của nó. Quy trình: [WORKFLOW.md, Phase 0](../../../WORKFLOW.md#phase-0--domain-discovery).

| Area | Note | Ticket | Unlocks | Status |
|---|---|---|---|---|
| A. COD cash flow | [cod-cash-flow.md](cod-cash-flow.md) | [#2](https://github.com/BuhDuy256/cod-sync/issues/2) | Các dòng glossary, rule lịch trả tiền (payout schedule), hình dạng của ledger | not started |
| B. Carrier statements and fees | [carrier-statements.md](carrier-statements.md) | [#3](https://github.com/BuhDuy256/cod-sync/issues/3) | Danh sách loại phí, rule định dạng bảng kê, use case "import bảng kê của carrier" | not started |
| C. Order statuses and carrier events | [carrier-events.md](carrier-events.md) | [#4](https://github.com/BuhDuy256/cod-sync/issues/4) | Danh sách trạng thái, các requirement nhận event, kiểm tra idempotency (P-5) | not started |
| D. Bank statements and transfers | [bank-transfers.md](bank-transfers.md) | [#5](https://github.com/BuhDuy256/cod-sync/issues/5) | Use case khớp giao dịch chuyển khoản và rule sai số cho phép (tolerance) | not started |
| E. Discrepancies and complaints | [discrepancies.md](discrepancies.md) | [#6](https://github.com/BuhDuy256/cod-sync/issues/6) | Danh mục loại chênh lệch (P-6), hạn khiếu nại, use case khiếu nại | not started |
| F. Ledger basics | [ledger-basics.md](ledger-basics.md) | [#7](https://github.com/BuhDuy256/cod-sync/issues/7) | Rule bất biến về tiền (P-4), decision về thiết kế ledger | not started |
| G. How shops reconcile today | [shop-practice.md](shop-practice.md) | [#8](https://github.com/BuhDuy256/cod-sync/issues/8) | Evidence cho các vision block W-1 đến W-3, actor và mục tiêu của use case | not started |
| H. Reference products | [reference-products.md](reference-products.md) | [#9](https://github.com/BuhDuy256/cod-sync/issues/9) | Phần Product evidence của mỗi use case | not started |

Câu hỏi được đánh số từ 1 đến 50 xuyên suốt các ticket. Note nhắc tới một câu hỏi bằng số của nó.

## Sources to start from

- API docs cho developer của các carrier: GHN, GHTK, J&T Express, Viettel Post.
- Trang help center của carrier về đối soát và khiếu nại, và điều khoản dịch vụ của carrier.
- Forum người bán và group Facebook của các shop online.
- Trang hướng dẫn của Sapo, Haravan và Nhanh.vn.
- Tài liệu nhập môn về kế toán kép (double-entry bookkeeping).
