# Gate: Business rule

Template: `_TEMPLATE.md`. Style: `../_STYLE.md`. Cited by: `../02-use-cases/`, `../03-requirements/fr/`, `../03-requirements/nfr/`, `../01-product-vision/`.

## 1. What a BR is, and is not

**BR định nghĩa một giá trị mà hành vi của product phụ thuộc vào.** Giá trị đó là allow-set, giới hạn, ngưỡng, quota, thời gian lưu, hoặc một danh sách định nghĩa "thế nào thì được tính". Hành vi áp dụng giá trị là FR. BR nói giá trị đó là gì.

> FR: "The system rejects a carrier statement that does not match a known format [BR-xxx]."
> BR-xxx: the accepted carriers, and the statement format of each carrier.

| If the content is... | Then it belongs |
|---|---|
| Hệ thống show, giữ, đổi, tạo hay từ chối điều gì, và khi nào | `../03-requirements/fr/`. FR cite BR này |
| Rule không có giá trị riêng, như "cannot close a period while an import is running" | `../03-requirements/fr/` |
| Một phán đoán của model không có giá trị viết ra được | `../03-requirements/fr/`, kèm evaluation criterion |
| Chỉ tiêu thời gian chờ, độ tin cậy, bảo mật, riêng tư hay khả năng tiếp cận | `../03-requirements/nfr/` |
| Mục tiêu, hành trình, step hay intent của user | `../02-use-cases/` |
| Hệ thống giữ hay kiểm tra giá trị bằng cách nào: code, storage, config | ADR hoặc công việc architecture |
| Product trông ra sao hay user thao tác thế nào | Công việc UI design (chưa có folder) |

Marker `[BR-?: topic]` gọi tên một chủ đề, không phải một decision. Khi viết rule ra có thể thấy chủ đề đó không có giá trị riêng. Marker chỉ được thay bằng BR khi BR cover đầy đủ nghĩa; nếu chỉ cover một phần thì marker ở lại và phần thiếu được báo ra.

### Granularity and values

- **Một BR** là một rule thống nhất. Các giá trị của nó chi phối một quyết định và thay đổi vì những lý do liên quan.
- **Nhiều giá trị** có thể chung một BR. Không tách một rule thống nhất chỉ vì nó có nhiều giá trị; không gộp các rule không liên quan để tiết kiệm file.
- **Không trùng.** Trước khi viết, tìm trong folder các statement và giá trị đã có.

Mỗi giá trị là một block `### V-n · name` với field Value. Giá trị chính xác: số kèm đơn vị; giới hạn ghi rõ có tính biên hay không giới hạn; danh sách ghi rõ đóng hay mở. Giá trị đủ chính xác để một FR criterion test được tại và vượt quá giá trị đó. Giá trị không chứa hành vi, hệ thống làm gì khi chạm giới hạn được viết trong FR.

### IDs and files

- Mỗi BR một file: `BR-xxx.md`. `xxx` là ba chữ số. `id` bằng tên file.
- ID mới đi sau ID cao nhất đang có hoặc đã xóa. ID không đổi khi title, câu chữ hay giá trị đổi; không dùng lại, không đánh số lại.
- ID chỉ bị bỏ khi rule rời khỏi behavior model hoặc được gộp vào BR khác. ID bị bỏ được ghi bên dưới kèm ngày và BR mà nó gộp vào.
- ID của giá trị là `V-1`, `V-2` trong một BR, không đánh số lại.

Removed BR IDs: none.

### Links

Link chỉ đi từ trên xuống. Use case (System hoặc When), FR, NFR hoặc vision cite BR bằng `[BR-xxx]`.

- BR không gọi tên use case, step, nhánh, FR hay NFR. Nó không cite BR khác.
- Muốn tìm chỗ cite một BR, tìm ID của nó trong các file spec.

### One source of truth

Một giá trị chỉ nằm trong đúng một BR. Các file spec khác không bao giờ nêu nó, diễn giải nó thành con số hay liệt kê các item được phép; chúng cite ID. Đổi giá trị chỉ đổi BR; trong cùng thay đổi đó, tìm các file cite BR có câu chữ dựa vào giá trị cũ, và báo ra từng file.

## 2. Criteria

Cột "Check" là tầng kiểm tra dự kiến: *Lint* = máy kiểm tra được, *Review* = người phán đoán, *CI* = đối chiếu chéo. Chưa có tool, nên review làm cả Lint lẫn CI.

| ID | Criterion | Prevents | Check |
|---|---|---|---|
| BRG-01 | BR định nghĩa giá trị của một rule mà hành vi product phụ thuộc vào. Không có hành vi, mục tiêu, hành trình, chỉ tiêu chất lượng, interface, architecture, tiến độ hay version | Hành vi bị viết hai lần; giá trị bị giấu trong hành vi | Review |
| BRG-02 | Độ chi tiết theo section 1: một rule thống nhất; cho phép các giá trị liên quan; tách khi hành vi/lý do không liên quan; không giá trị nào được định nghĩa hai lần | File rule khổng lồ; cùng giá trị ở hai chỗ | Review |
| BRG-03 | Mỗi giá trị chính xác: số kèm đơn vị; giới hạn có tính biên hay không; danh sách đóng hay mở. FR test được tại và vượt quá giá trị | Hai người áp dụng một giá trị theo hai kiểu | Review |
| BRG-04 | File theo `_TEMPLATE.md`: frontmatter có `id` và `title`; các field của Rule theo thứ tự; ít nhất một value block. `Why` trống thì bỏ dòng. `Undecided` và `Notes` bỏ khi trống | File không so sánh hay kiểm tra được | Lint (fields, order) |
| BRG-05 | Giá trị chưa quyết ghi `not set`. Không đoán số, khoảng hay "khoảng chừng". Không file nào trình bày nó như giới hạn đã duyệt | Giới hạn bịa ra; giá trị còn mở bị đọc như đã quyết | Lint (`not set`) + Review |
| BRG-06 | Section `Undecided` nêu một khía cạnh còn mở mà không phải giá trị, một dòng, kết thúc bằng "Pending decision.". Giá trị chưa quyết là `not set`, không phải item ở đây | Câu hỏi còn mở biến thành rule trước khi được quyết | Review |
| BRG-07 | Một giá trị nằm trong một BR. Use case, FR, NFR và vision cite ID, không nêu lại giá trị. Marker chỉ được thay khi BR cover đầy đủ nghĩa | Cùng giá trị trong nhiều file; marker bị xóa bởi một chủ đề na ná | Lint (numbers in citing files) + CI (ID exists) + Review |
| BRG-08 | Tên file `BR-xxx.md` có ba chữ số, bằng `id` trong frontmatter. ID là duy nhất và không đánh số lại. ID bị bỏ được ghi ở section 1, không dùng lại. BR không gọi tên use case, step, nhánh, FR, NFR hay BR khác | Một ID mang hai nghĩa; link trỏ ngược lên | Lint (name, format) + CI (unique) |
| BRG-09 | Text theo rule 1–10 của `../_STYLE.md` trong Statement và Value. Không interface (rule 11) | Rule đọc hiểu hai kiểu; design bị khóa qua một rule | Lint (banned words) + Review |

## 3. Illustrations

**BRG-01: phán đoán không phải giá trị.**

> Fail: BR "the system asks when the source is unclear". Đó là hành vi kèm phán đoán, tức là FR.
> Pass: quyết định rằng có một danh sách các loại source được chấp nhận. BR liệt kê các loại đó.

**BRG-07: một chỗ cho một giá trị.**

> Fail: use case ghi "The system backs off a few seconds on interruption [BR-000]."
> Pass: "The system backs off by the back-off limit [BR-000]." Con số nằm trong BR-000.
