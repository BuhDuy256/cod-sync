# Gate: Product vision

Template: `_TEMPLATE.md`. Style: `../_STYLE.md`. Children: `../02-use-cases/`, `../03-requirements/`, `../04-business-rules/`.

## 1. What the vision is, and is not

**Vision định nghĩa product là gì, trước khi bất kỳ file spec nào khác mô tả nó làm gì.** Vision trả lời năm câu hỏi: (1) Product là gì? (2) Nó giải quyết vấn đề gì? (3) Giá trị chính nó mang lại là gì? (4) Nguyên tắc nào định hướng các lựa chọn? (5) Ranh giới nào thuộc về bản chất của product?

**Vision không phải decision log, danh sách feature hay scope.** Nó chỉ giữ những gì vẫn đúng khi scope, interface hay architecture thay đổi (VG-01).

**Vision không lớn lên bằng suy luận.** Một statement chỉ được confirm khi chủ product nói ra. Mọi thứ khác là đề xuất hoặc câu hỏi mở (VG-13). Chỗ trống được ghi là chỗ trống (VG-14).

### Where content belongs

| If the content is... | Then it belongs |
|---|---|
| Product là gì, vì sao tồn tại, giá trị, nguyên tắc, ranh giới lâu dài | Ở đây |
| Một năng lực mà product cung cấp | `../02-use-cases/`. Chỉ đưa vào đây khi đã khẳng định nó là một phần bản chất của product |
| Một step, một response hay một nhánh của một mục tiêu | `../02-use-cases/` |
| Một câu test được về system response | `../03-requirements/fr/` |
| Thời gian chờ, chỉ tiêu kích thước hay chỉ tiêu chất lượng khác | `../03-requirements/nfr/`. Vision cite `[NFR-?: topic]` |
| Giới hạn, allow-list, loại file hay giá trị khác do rule định nghĩa | `../04-business-rules/`. Vision cite `[BR-?: topic]` |
| Code đạt được điều gì đó bằng cách nào: engine, storage, framework, protocol | Decision record trong `docs/decisions/` |
| Product được thao tác ra sao hay trông thế nào | Công việc UI design (chưa có folder) |
| Rule viết file spec, hoặc thuật ngữ dùng chung | `../_STYLE.md` hoặc `AGENTS.md` |
| Quan sát thô về một product khác | `docs/research/` |

### A boundary is not a scope limit

Boundary nói product KHÔNG phải là gì, theo bản chất của nó. Nó đúng ở mọi release. Scope limit nói một release bỏ ra ngoài những gì. Chỉ cái đầu tiên thuộc về đây.

> Scope limit (không ở đây): "V1 is web-only."
> Boundary (ở đây): "The product does not move real money; it simulates holding and releasing it."

Kiểm tra: nếu có thời gian vô hạn, statement có còn đúng không? Nếu không, đó là scope limit.

### Confirmed, proposed, open

Mỗi statement có một trong hai status.

| Status | Meaning | Lower spec may rely on it |
|---|---|---|
| `confirmed` | Chủ product đã nói ra | Yes |
| `proposed` | Mới là đề xuất, chưa được quyết | No |

Câu hỏi mở là trạng thái thứ ba: chưa biết đủ để quyết.

### Link direction: top-down only

Vision nằm trên cùng của chuỗi. File spec cấp dưới không bao giờ gọi tên một vision block. Muốn kiểm tra một file với vision thì đọc vision.

### One source of truth

Một sự thật được viết trong đúng một block. Các block khác trỏ tới nó bằng ID. Term hay region mà `../_STYLE.md` định nghĩa thì dùng ở đây, không định nghĩa lại (VG-06).

## 2. Sections, blocks, and IDs

| Section | Answers | Block ID | Fields |
|---|---|---|---|
| What the product is | Question 1 | `I-x` | Statement, Status, Source, Spec implications |
| Why it exists | Questions 2 and 3 | `W-x` | Statement, Status, Source, Evidence, Spec implications |
| Principles | Question 4 | `P-x` | Statement, Status, Source, Why, Spec implications |
| Boundaries | Question 5 | `B-x` | Statement, Status, Source, Why, Spec implications |
| Open questions | Any gap | `Q-x` | Question, Affects |
| Removed | Removed IDs | none | One line per ID |

- `Status` là `confirmed` hoặc `proposed`. Luôn có mặt.
- `Source` chỉ xuất hiện khi `proposed`: nói đề xuất đến từ đâu và được suy ra từ cái gì.
- `Why` ghi lý do, hoặc bỏ dòng. Không bịa lý do.
- `Spec implications` chỉ xuất hiện ở block `confirmed`, và chỉ ghi những gì suy ra trực tiếp từ statement.
- ID không bao giờ đánh số lại hay dùng lại. Block bị xóa được ghi trong `Removed` (VG-05).

## 3. Criteria

Cột "Check" là tầng kiểm tra dự kiến: *Lint* = máy kiểm tra được, *Review* = người phán đoán, *CI* = đối chiếu chéo. Chưa có tool, nên review làm cả Lint lẫn CI.

| ID | Criterion | Prevents | Check |
|---|---|---|---|
| VG-01 | Mỗi block nói product là gì, vì sao tồn tại, giá trị của nó, một nguyên tắc, hoặc một ranh giới lâu dài. Nó vẫn đúng khi scope, interface hay architecture thay đổi. Sự thật chỉ một feature hay use case phụ thuộc thì đi theo use case đó | Vision biến thành danh sách feature | Review |
| VG-02 | Block nói điều gì đúng về product hoặc với user. Nó không bao giờ nói code đạt được điều đó bằng cách nào. `Why` ghi lý do thật, hoặc bỏ dòng | Architecture bị chọn một cách tình cờ | Review |
| VG-03 | Boundary nói product KHÔNG phải là gì theo bản chất, qua phép kiểm tra ở section 1. Feature còn thiếu hay scope limit không phải boundary | Giới hạn của V1 trở thành giới hạn vĩnh viễn | Review |
| VG-04 | Câu hỏi mở có `Question` và `Affects`. `Affects` liệt kê bằng ID các spec item đang chờ câu trả lời, hoặc "none yet". Không block nào khác trả lời câu hỏi | Chỗ trống bị giấu trong một statement | Lint (fields) + Review |
| VG-05 | ID `I-x`, `W-x`, `P-x`, `B-x`, `Q-x` không bao giờ đánh số lại hay dùng lại. Block bị xóa được ghi trong `Removed` kèm nội dung đã chuyển đi đâu | Citation trỏ sai block | Review |
| VG-06 | Mỗi sự thật được viết một lần. Các block khác trỏ bằng ID. File không định nghĩa lại term, region hay rule mà `../_STYLE.md` đã định nghĩa | Hai nguồn cho một sự thật lệch nhau | Review |
| VG-07 | Mỗi block có `Status: confirmed` hoặc `proposed`. Block `proposed` có `Source` và không có `Spec implications`. Spec cấp dưới không dựa vào block `proposed` | Đề xuất bị đọc như rule | Lint (fields) + Review |
| VG-08 | File không chứa scope, thứ tự hay độ ưu tiên. Không dùng MVP, V1, phase, roadmap | Quyết định scope đặt sai chỗ | Lint (words) + Review |
| VG-09 | File không chứa giá trị rule hay chất lượng. Nó cite `[BR-?: topic]` hoặc `[NFR-?: topic]` cho mọi giới hạn hay target | Cùng một rule viết ở nhiều chỗ | Lint (numbers, markers) + CI (ID exists) |
| VG-10 | Link chỉ đi từ trên xuống. Chỉ `Affects` gọi tên spec item cấp dưới, và mỗi ID đều tồn tại hoặc đã bị xóa | Link trỏ ngược lên; ID treo | CI (reference exists) |
| VG-11 | Text theo `../_STYLE.md`: từ trong glossary, không có động từ mơ hồ bị cấm, mỗi dòng một sự thật, evidence một dòng riêng | Text đọc hiểu hai kiểu | Lint (banned words) + Review |
| VG-12 | File không có văn quảng cáo. Không dùng từ khen như powerful, smooth, intuitive, smart, best, easy | Văn quảng cáo bị đọc như cam kết | Lint (words) + Review |
| VG-13 | Chỉ chủ product confirm một statement. Nội dung mới chỉ được viết dưới dạng block `proposed` hoặc câu hỏi mở. Nội dung tìm thấy trong use case, research link hay reference product không vì thế mà thành confirmed | Suy luận và feature đi mượn trở thành sự thật của product | Review |
| VG-14 | Block `W-x` nêu một vấn đề, nhu cầu hay giá trị của con người có `Evidence` với tag từ `../_STYLE.md`. Nó không nói quá bằng chứng. Chỉ có `[assumed]` thì viết như một niềm tin ("I believe that..."). Phần chưa có gì ghi "Not written yet. See Q-x." | Vấn đề của user bị bịa ra; vision trông hoàn chỉnh nhưng toàn đoán | Lint (fields, tags) + Review |

## 4. Illustrations

**VG-01: bản chất, không phải feature.**

> Fail: "The product imports carrier statements." Đó là một năng lực; nó thuộc về use case.
> Pass: "The product is a web-hosted system, with accounts, that reconciles cash-on-delivery money for a shop sending parcels through two or more carriers."

**VG-03: boundary, không phải giới hạn của V1.**

> Fail: "Boundary: no AI explanation of discrepancies." V1 chọn không làm; đó là scope.
> Pass: "Boundary: the product does not keep inventory; it records only whether a return arrived."
