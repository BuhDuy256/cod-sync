# Gate: Use case

Template: `_TEMPLATE.md`. Style: `../_STYLE.md`. Children: `../03-requirements/fr/`, `../03-requirements/nfr/`, `../04-business-rules/`.

## 1. What a use case is, and is not

**Use case mô hình hóa hành vi của product cho một mục tiêu của user, đạt được trong một lần ngồi.** Nó nói user làm gì và product phản hồi thế nào theo cách quan sát được. Mỗi system response là một functional requirement ứng viên. Mỗi alternative flow là một requirement ứng viên cho lỗi/trường hợp biên. Mỗi rule hay chỉ tiêu chất lượng mà một step phụ thuộc được cite ở đây và định nghĩa ở chỗ khác.

**Flow ghi lại hành vi cần cân nhắc, không phải cam kết sẽ build.** Use case khám phá rộng. Evidence cho biết ý tưởng đến từ đâu; nó không chọn gì cả.

### Where content belongs

| If the content is... | Then it belongs |
|---|---|
| Giới hạn, ngưỡng, quota, allow-list, thời gian lưu, hay giá trị khác do rule định nghĩa | `../04-business-rules/`. Use case cite ID của rule |
| Thời gian chờ, chỉ tiêu kích thước, availability, hay chỉ tiêu chất lượng khác | `../03-requirements/nfr/`. Use case cite ID của NFR |
| Một câu test được về system response | `../03-requirements/fr/`. Use case cite ID của requirement |
| Quan sát thô từ transcript (product làm gì, hiển thị giới hạn nào) | `docs/research/`. Use case link tới research item |
| Hệ thống đạt được response bằng cách nào (model, queue, storage, API) | ADR hoặc công việc architecture, không phải ở đây |
| User thao tác product thế nào hoặc nó trông ra sao: control, thao tác, vị trí, label, màu, layout | Công việc UI design (chưa có folder). Use case chỉ viết intent và response (UCG-09) |

### Link direction: top-down only

- Vision (`../01-product-vision/`) là cha. Vision không liệt kê use case; muốn tìm cha thì đọc vision.
- Use case cite ID của requirement, NFR và rule. Requirement, NFR và rule không bao giờ cite use case, step hay nhánh.
- Use case link tới các research item hỗ trợ nó. Research item không gọi tên use case.

### Use case IDs

- Một ID (`UC-xxx`) đặt tên cho một file use case. Một flow ID (`Sx`, `Ax`) đặt tên cho một block trong file.
- Namespace là `docs/spec/`.
- Một ID không bao giờ chuyển sang mục tiêu khác hay được dùng lại, kể cả sau khi file bị xóa.
- ID mới lấy số liền sau ID cao nhất trong folder và trong danh sách ID đã xóa. Khoảng trống giữ nguyên.
- ID không bị đánh số lại.

Removed use case IDs: none.

## 2. Evidence tags

Nhận định về hành vi của product dùng tag từ `../_STYLE.md` (`[observed: <source>]`, `[inferred: <source>]`, `[assumed]`). Với product coverage, source là một research item hoặc transcript trong `docs/research/`. Flow chưa ai ghi lại là `unverified` và các step của nó giữ `[assumed]`.

Evidence cho biết flow hay response đến từ đâu. Nó không phải quyết định build. Một research item cho thấy hành vi trong product khác không tự động đưa hành vi đó vào scope.

## 3. Criteria

Cột "Check" là tầng kiểm tra dự kiến: *Lint* = máy kiểm tra được, *Review* = người phán đoán, *CI* = đối chiếu chéo. Chưa có tool, nên review làm cả Lint lẫn CI.

| ID | Criterion | Prevents | Check |
|---|---|---|---|
| UCG-01 | Một mục tiêu của user, đạt được trong một lần ngồi, có kết quả quan sát được và có giá trị. Title là user + động từ + đối tượng cụ thể + điểm phân biệt, bằng lời của user | Case quá to hoặc quá nhỏ; hai case không phân biệt được | Review |
| UCG-02 | Situation and goal mô tả user muốn gì và vì sao là lúc này. Không có feature hay giải pháp | Giải pháp đội lốt mục tiêu | Review |
| UCG-03 | Bảng Steps có 3–9 dòng `Sx` theo thứ tự. Mỗi dòng có User (intent), System (quan sát được, không có "if"), FR (ID hoặc `FR-?`). Không có settings, không có interface | Response bị chôn trong văn xuôi; không rõ FR đến từ đâu | Lint (rows, columns) + Review |
| UCG-04 | Mỗi alternative là một block `### Ax · name` với At, Ends, When, System, FR. `Ends` dùng một giá trị trong template. Mỗi step nhận input, có thể bị hủy, phụ thuộc service bên ngoài, hoặc có thể chậm thì có alternative, hoặc có lý do được ghi lại | Nhánh không test lại được | Lint (fields) + Review |
| UCG-05 | Outcome kiểm chứng được bằng quan sát. Minimal guarantee nói điều gì vẫn đúng khi bất kỳ nhánh nào thất bại | Không có kết luận cuối để test; mất dữ liệu khi lỗi | Review |
| UCG-06 | ID của step và nhánh không bị đánh số lại sau khi đã được cite; ID bị bỏ được liệt kê và không dùng lại. Mỗi tham chiếu tới use case hay block khác (một `Ends`, một "like UC-xxx Sx") gọi tên một ID có tồn tại và chưa bị bỏ. Cho phép `UC-?` trong `Ends` | Citation trỏ sai; tham chiếu tới block đã bỏ | CI (references) + Review |
| UCG-07 | Use case không chứa giá trị của rule hay chất lượng. Nó cite bằng ID mọi requirement, giới hạn, allow-list, kiểm tra hay thời gian chờ mà một step phụ thuộc (`FR-xxx`, `[BR-xxx]`, `[NFR-xxx]`). Cho phép marker `?` ở mọi flow | Một rule nằm ở nhiều chỗ; giá trị đổi ở chỗ này mà không đổi ở chỗ kia | Lint (numbers, markers) + CI (ID exists) |
| UCG-08 | Product coverage ghi cho mỗi reference product là `observed`, `none` hoặc `unverified`, kèm research link. Khác biệt được mô tả bằng văn xuôi, không bằng giá trị rule. Nhận định chưa ghi lại giữ `[assumed]` | Đoán mà đọc thành sự thật | Lint (tags) + Review |
| UCG-09 | Text theo `../_STYLE.md`: từ trong glossary, không có động từ mơ hồ bị cấm, không có "can/should/might" trong System, điều kiện nằm trong When, mỗi dòng một hành động, evidence một dòng riêng. Use case viết intent và response, không viết widget, thao tác, vị trí, style hay label; chỉ gọi tên một chỗ bằng region | Response đọc hiểu hai kiểu; spec vỡ khi design đổi | Lint (banned words, interface words) + Review |
| UCG-10 | Interaction diagram theo `../_MERMAID.md` (MG-01..MG-10): hợp lệ, là view được generate từ bảng Steps và Alternative flows, mỗi message map 1-1, không sửa tay | Diagram lệch khỏi source; mất nhánh khi vẽ | Review (cho tới khi có skill), sau đó CI |

## 4. Illustrations

**UCG-03: quan sát được, không phải settings.**

> Fail: "S5: the parser reads the CSV and the worker writes rows to the ledger table."
> Pass: "S5 · System: shows each order in the statement with its collected COD and fees."

**UCG-04: nhánh phát hiện được.**

> Fail: "A1: there is an error. The system shows the error."
> Pass: "A1 (at S3): the file does not match a known statement format. The system keeps the last imported statement and reports which format it expected."

**UCG-09: intent và response, không phải interface.**

> Fail: "The user clicks the Import button in the top corner."
> Pass: "The user requests an import. The system reads the carrier statement and shows the orders it settles."
