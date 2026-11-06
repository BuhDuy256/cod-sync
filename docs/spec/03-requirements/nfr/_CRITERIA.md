# Gate: Non-functional requirement

Template: `_TEMPLATE.md`. Style: `../../_STYLE.md`. Cited by: `../../02-use-cases/`, `../fr/`, `../../01-product-vision/`. Rule values: `../../04-business-rules/`.

## 1. What an NFR is, and is not

**NFR là một ràng buộc chất lượng ở cấp product.** Nó nói product phải nhanh, tin cậy, bảo mật, riêng tư, chính xác hay dễ tiếp cận tới mức nào, dưới một điều kiện đã nêu. NFR được kiểm chứng bằng cách đo so với một target, hoặc kiểm tra một thuộc tính bắt buộc.

### When to write an NFR

Một đại lượng đo được không tự nó cần NFR. Chỉ viết NFR khi đủ cả bốn điều kiện:

1. Một cam kết của product cần chất lượng đó, hoặc một rủi ro đã nêu của product biện minh cho nó.
2. Chất lượng đó đo được hoặc kiểm tra được.
3. Nó thêm một ràng buộc chất lượng độc lập ở cấp product; nó không chỉ lặp lại hành vi hay acceptance criterion của một FR.
4. Target làm thay đổi chất lượng product đối với user. User không cần thấy nó: ràng buộc về bảo mật, riêng tư và độ tin cậy bảo vệ user mà không cần hiển thị.

Đại lượng không qua được điều kiện đầu tiên thì ở lại trong FR, UI hoặc công việc engineering. Hành vi mang ý nghĩa bảo mật (như không hiển thị key) là FR. Chỉ tiêu chất lượng của output model chỉ là NFR khi nó được biến thành cam kết của product.

### Where content belongs

| If the content is... | Then it belongs |
|---|---|
| Hệ thống show, giữ, đổi, tạo hay từ chối điều gì, và khi nào | `../fr/`. FR cite NFR này |
| Allow-set, giới hạn, quota, thời gian lưu do rule định nghĩa | `../../04-business-rules/` |
| Mục tiêu, hành trình hay step của user | `../../02-use-cases/` |
| Metric mà team dùng để build/chạy code, không hứa với user | Không nằm trong spec. Công việc engineering |
| Ngưỡng dùng để so sánh/chọn/tune model trong lúc research | Không nằm trong spec. Công việc research |
| Hệ thống đạt target bằng cách nào: engine, storage, framework, tool | ADR hoặc công việc architecture |
| Product trông ra sao hay user thao tác thế nào | Công việc UI design (chưa có folder) |

### Granularity and measures

- **Một NFR** cover một thuộc tính chất lượng cho một phần thống nhất của product.
- **Nhiều measure** có thể chung một NFR khi chúng kiểm tra cùng một chất lượng dưới các điều kiện khác nhau.
- **Tách** NFR khi nó gộp nhiều thuộc tính chất lượng, hoặc một phần product thay đổi vì những lý do không liên quan.
- **Không trùng.** Trước khi viết, tìm trong folder các statement đã có.

Mỗi measure là một block `### M-n · name` với Condition, Measure, How to measure, Target, Passes when. `Condition`, `Measure`, `How to measure` phải đủ rõ để kiểm chứng; `Target` và `Passes when` được để `not set` khi chưa quyết. Không đoán một con số, một khoảng hay "khoảng chừng" (NFG-04).

### IDs and files

- Mỗi NFR một file: `NFR-xxx.md`. `xxx` là ba chữ số. `id` bằng tên file.
- ID mới đi sau ID cao nhất đang có hoặc đã xóa. ID không đổi khi title hay target đổi, không dùng lại, không đánh số lại.
- ID chỉ bị bỏ khi requirement rời khỏi behavior model hoặc được gộp vào NFR khác. ID bị bỏ được ghi bên dưới kèm ngày và NFR mà nó gộp vào.
- ID của measure là `M-1`, `M-2` trong một NFR, không đánh số lại.

Removed NFR IDs: none.

### Links

Link chỉ đi từ trên xuống. Use case (System hoặc When), FR hoặc vision cite NFR bằng `[NFR-xxx]`.

- NFR không gọi tên use case, step, nhánh, FR hay NFR khác. Nó được cite BR trong Condition.
- Muốn tìm chỗ cite một NFR, tìm ID của nó trong các file spec.

### One source of truth

Một target chỉ nằm trong đúng một NFR. Use case, FR hay vision không bao giờ nêu nó hay diễn giải nó thành con số; chúng cite ID. Marker `[NFR-?: topic]` chỉ được thay bằng `[NFR-xxx]` khi NFR cover đầy đủ nghĩa của marker; nếu chỉ cover một phần thì marker ở lại và phần thiếu được báo ra.

## 2. Criteria

Cột "Check" là tầng kiểm tra dự kiến: *Lint* = máy kiểm tra được, *Review* = người phán đoán, *CI* = đối chiếu chéo. Chưa có tool, nên review làm cả Lint lẫn CI.

| ID | Criterion | Prevents | Check |
|---|---|---|---|
| NFG-01 | NFR nêu một chất lượng cấp product dưới một điều kiện đã nêu. Nó thêm ràng buộc riêng, không lặp lại FR. Không có giá trị rule, mục tiêu, hành trình, interface, architecture, metric engineering, tiến độ hay version | Hành vi hay giới hạn bị viết hai lần | Review |
| NFG-02 | NFR qua được bốn điều kiện ở section 1 | Viết NFR cho mọi chất lượng theo thói quen | Review |
| NFG-03 | Độ chi tiết theo section 1: một thuộc tính cho một phần thống nhất; nhiều measure cho cùng chất lượng; không trùng | NFR khổng lồ; cùng target nằm ở hai file | Review |
| NFG-04 | File theo `_TEMPLATE.md`: frontmatter có `id` và `title`; các field của Requirement theo thứ tự; ít nhất một measure. Chỉ `Target` và `Passes when` được `not set`. `Why` trống thì bỏ dòng. `Undecided` và `Notes` bỏ khi trống | File không so sánh hay kiểm tra được | Lint (fields, order) |
| NFG-05 | Mỗi measure được định nghĩa đầy đủ: Condition làm lại được, Measure và How to measure đủ để kiểm chứng. Target có đơn vị và giới hạn, hoặc là một thuộc tính bắt buộc. Ranh giới product-controlled hay end-to-end và các điều kiện phụ thuộc provider được nêu rõ; thời gian của provider không bị giấu đi. Không tool, không architecture | Requirement không kiểm chứng được; thời gian của provider bị hứa như kết quả của product | Review |
| NFG-06 | Target chưa quyết ghi `not set` ở Target và Passes when. Không đoán số, khoảng hay "khoảng chừng". Không file nào trình bày nó như target đã duyệt | Target bịa ra; target còn mở bị đọc như đã quyết | Lint (`not set`) + Review |
| NFG-07 | Section `Undecided` nêu một khía cạnh còn mở mà không phải target, một dòng, kết thúc bằng "Pending decision." hoặc "Pending technical evidence." cho định nghĩa còn thiếu bằng chứng. Target còn thiếu là `not set`, không phải item ở đây | Câu hỏi còn mở biến thành target trước khi được quyết | Review |
| NFG-08 | Tên file `NFR-xxx.md` có ba chữ số, bằng `id` trong frontmatter. ID là duy nhất và không đánh số lại. ID bị bỏ được ghi ở section 1, không dùng lại. NFR không gọi tên use case, step, nhánh, FR hay NFR khác | Một ID mang hai nghĩa; link trỏ ngược lên | Lint (name, format) + CI (unique) |
| NFG-09 | Text theo rule 1–10 của `../../_STYLE.md` trong Statement, Condition, Measure và Target. Không interface (rule 11) | Requirement đọc hiểu hai kiểu; design bị khóa qua một chỉ tiêu chất lượng | Lint (banned words) + Review |

## 3. Illustrations

**NFG-05: một measure do product kiểm soát.**

> NFR-000 · Quality attribute: performance · Statement: the accountant sees the result of a carrier statement import soon after the file is received.
> M-1 · Condition: the file is already received by the system, from a simulated carrier. Boundary: product-controlled — measure from the system receiving the file to the result being shown, not the upload time over the user's network.
> Measure: time from file received to result shown. How to measure: repeat the import with the same file.

**NFG-02: không phải đại lượng nào cũng là NFR.**

> Fail: một NFR cố định mức dùng memory lúc runtime của hệ thống. Không cam kết hay rủi ro nào của product cần nó.
> Pass: không có NFR. Team theo dõi nó như công việc engineering, ngoài spec.
