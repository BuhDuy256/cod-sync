# Gate: Mermaid

Áp dụng cho mọi Mermaid diagram nhúng trong `docs/spec/` (sequence diagram của use case và mọi flowchart hay state diagram khác). Diagram là một **view**: nguồn sự thật là các text block. Không bao giờ sửa tay diagram để nó "khớp".

Cột "Check" là tầng kiểm tra dự kiến: *Lint* = máy kiểm tra được, *Review* = người phán đoán, *CI* = đối chiếu chéo. Chưa có tool, nên hiện tại review làm cả Lint lẫn CI.

| ID | Criterion | Prevents | Check |
|---|---|---|---|
| MG-01 | Cú pháp Mermaid hợp lệ, render được trên GitHub và VS Code (tập con an toàn trong skill `mermaid-markdown`) | Diagram bị vỡ khi xem | Lint |
| MG-02 | Diagram là view. Source block là sự thật. Sửa source rồi generate lại diagram, không sửa diagram cho khớp source | Hai nguồn lệch nhau | CI |
| MG-03 | Mỗi participant/node/message map 1-1 với một phần tử của source. Không thừa, không thiếu, không trùng | Diagram không còn là view trung thực | CI |
| MG-04 | Label ngắn, một nghĩa, theo language policy (`_STYLE.md`); ID giữ tiếng Anh | Một label hai người đọc hiểu hai kiểu | Review |
| MG-05 | Không hardcode màu, theme, class, HTML hay style. Đọc được trên cả nền sáng và nền tối | Diagram chỉ đẹp trên một theme | Lint |
| MG-06 | Nhánh dùng đúng cấu trúc Mermaid (`alt`/`opt`/`loop`), không bị "làm phẳng" tới mức mất nghĩa. Nhánh không vẽ gọn được (ví dụ "back to S2") được ghi chú dưới diagram | Mất nhánh khi vẽ | Review |
| MG-07 | Chiều mũi tên đúng (user → system là request, system → user là response). Mỗi participant được khai báo đúng một lần | Đọc sai tương tác vì sai chiều | Review |
| MG-08 | Diagram trả lời câu hỏi chính chỉ trong một cái nhìn. Chi tiết phụ để trong văn xuôi | Diagram thành một bức tường chữ | Review |
| MG-09 | Thay đổi source block thì generate lại diagram trong cùng thay đổi đó | Diagram tụt lại sau source | CI |
| MG-10 | Không dùng tính năng beta hoặc tính năng renderer đích không hỗ trợ | Diagram chỉ chạy trên một renderer | Review |

## Illustrations

**MG-03 và MG-06: diagram trung thực, có nhánh.**

> Fail: sequence diagram chỉ vẽ main flow và bỏ nhánh "lost connection" vì nó là `Returns to S2`.
> Pass: main flow được vẽ tuyến tính; dưới diagram có `*Not drawn (back-to-step branch): A3.*`, và block `A3` vẫn giữ đủ `At/Ends/When/System`.

**MG-04: label một nghĩa, không phải interface.**

> Fail: `User->>System: click the Import button` — label mô tả một widget.
> Pass: `User->>System: request an import` — label là intent.
