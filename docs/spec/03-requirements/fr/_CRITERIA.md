# Gate: Functional requirement

Template: `_TEMPLATE.md`. Style: `../../_STYLE.md`. Cited by: `../../02-use-cases/` (cột FR). Rule values: `../../04-business-rules/`. Quality targets: `../nfr/`.

## 1. What an FR is, and is not

**FR là một câu test được về hành vi của hệ thống dưới một điều kiện đã nêu.** Nó nói hệ thống show, giữ, đổi, tạo hay từ chối điều gì. Response trong use case nói user quan sát được gì trong một hành trình; FR thêm độ chính xác mà test cần: input nào, kết quả nào, trường hợp biên nào, điều gì giữ nguyên.

| If the content is... | Then it belongs |
|---|---|
| Mục tiêu, hành trình, thứ tự step hay intent của user | `../../02-use-cases/`. Use case cite FR trong cột FR |
| Giới hạn, ngưỡng, quota, allow-list, thời gian lưu | `../../04-business-rules/`. FR cite `[BR-xxx]`, hoặc `[BR-?: topic]` cho tới khi rule có |
| Thời gian chờ, chỉ tiêu kích thước, availability | `../nfr/`. FR cite `[NFR-xxx]`, hoặc `[NFR-?: topic]` |
| User thao tác thế nào hoặc nó trông ra sao | Công việc UI design (chưa có folder) |
| Hệ thống đạt được hành vi bằng cách nào (model, queue, storage, API) | ADR hoặc công việc architecture |
| Build gì, hoặc đã build/test tới đâu | Không nằm trong spec. FR không có tiến độ, độ ưu tiên hay version |

Rule không có giá trị thì ở lại trong FR, ví dụ "the user cannot close a period while an import is running". Rule có giá trị thì chuyển sang `../../04-business-rules/`.

### Granularity and reuse

- **Một FR** có một mục đích thống nhất; các kết quả của nó đi cùng nhau và thay đổi vì cùng một lý do.
- **Tách** FR khi: các kết quả có thể thất bại độc lập dưới những điều kiện khác nhau có ý nghĩa; block khác chỉ cần một phần của nó; nó gộp các trách nhiệm không liên quan.
- **Dùng lại** FR khi block khác cần cùng hành vi: cùng loại điều kiện, cùng kết quả mong đợi.
- **Cùng chữ không có nghĩa là cùng hành vi.** Chỉ dùng lại khi nghĩa giống nhau.
- **Không có FR trùng.** Trước khi viết, tìm trong folder các statement đã có.
- **Độ chính xác.** FR có thể nêu hành vi cốt lõi; acceptance criterion thêm ít nhất một trong các thứ: kết quả quan sát được, điều kiện input liên quan, trường hợp biên, bảo đảm luôn đúng, hành vi khi lỗi. FR chỉ lặp lại use case thì không viết.

### IDs and files

- Mỗi FR một file: `FR-xxx.md`. `xxx` là ba chữ số. `id` trong frontmatter bằng tên file.
- ID mới lấy số liền sau ID cao nhất trong folder và trong các ID đã xóa. Khoảng trống giữ nguyên.
- ID không đổi khi title hay câu chữ đổi, và không được dùng lại.
- ID chỉ bị bỏ khi hành vi rời khỏi behavior model hoặc được gộp vào FR khác. ID bị bỏ được ghi bên dưới kèm ngày và, nếu gộp, FR mà nó gộp vào.
- ID của acceptance criterion là `AC-1`, `AC-2` trong một FR, không đánh số lại.

Removed FR IDs: none.

### Links

Link chỉ đi từ trên xuống. Use case cite FR trong cột FR của bảng Steps. Một FR có thể phục vụ nhiều block; một block có thể cite nhiều FR.

- FR không gọi tên use case, step hay nhánh.
- Muốn tìm các block dùng một FR, tìm ID của nó trong `../../02-use-cases/`.
- FR thay đổi cùng các block mà nó phục vụ. Thay đổi nghĩa của FR được kiểm tra với mọi block cite nó, trong cùng thay đổi đó.

## 2. Criteria

Cột "Check" là tầng kiểm tra dự kiến: *Lint* = máy kiểm tra được, *Review* = người phán đoán, *CI* = đối chiếu chéo. Chưa có tool, nên review làm cả Lint lẫn CI.

| ID | Criterion | Prevents | Check |
|---|---|---|---|
| FRG-01 | FR nêu một hành vi của hệ thống dưới một điều kiện đã nêu. Không có mục tiêu, hành trình, giá trị rule, chỉ tiêu chất lượng, interface, architecture, tiến độ hay version | Requirement lặp lại hành trình; một giá trị nằm ở hai chỗ | Review |
| FRG-02 | Độ chi tiết theo section 1: một mục đích thống nhất; tách có lý do; dùng lại cho cùng hành vi; không có FR thứ hai cho hành vi mà một FR đã cover | FR khổng lồ; mỗi step một FR theo thói quen; cùng hành vi viết hai lần | Review |
| FRG-03 | Acceptance criterion thêm độ chính xác test được ngoài response của use case: kết quả, input, biên, bất biến, hành vi khi lỗi | FR chỉ chép use case, không thêm được test nào | Review |
| FRG-04 | File theo `_TEMPLATE.md`: frontmatter có `id` và `title`; các field của Requirement theo thứ tự; ít nhất một acceptance criterion. `Why` trống thì bỏ dòng. `Undecided` và `Notes` bỏ khi trống. Không có field version, priority, progress, evidence hay use case | File không so sánh hay kiểm tra được | Lint (fields, order) |
| FRG-05 | `Status` là `confirmed` hoặc `proposed`. Block `proposed` có `Why` | Trạng thái duyệt mà không ai định nghĩa | Lint (value, fields) |
| FRG-06 | FR không chứa giá trị rule hay chỉ tiêu chất lượng. Nó cite `[BR-xxx]`/`[NFR-xxx]`, hoặc marker `?`. Cho phép input ví dụ trong criterion | Cùng một giá trị nằm trong nhiều file | Lint (numbers, markers) + CI (ID exists) |
| FRG-07 | Section `Undecided` nêu các hành vi còn mở, mỗi cái một dòng. Không statement hay criterion nào giả định kết quả cho chúng. Response phụ thuộc hoàn toàn vào một decision còn mở thì không có FR; block giữ `FR-?` | Câu hỏi còn mở biến thành requirement trước khi được quyết | Review |
| FRG-08 | Mỗi criterion là một block `### AC-n · name` với Given, When, Then, Check. `Check` là `deterministic` hoặc `evaluation`. `Then` là kết quả quan sát được, mỗi thứ một dòng, không có "if". Nó không ghim câu chữ chính xác của model | Criterion không test được; test bị buộc vào câu chữ của model | Lint (fields, values) + Review |
| FRG-09 | Text theo rule 1–10 của `../../_STYLE.md` trong Statement và Then, và tinh thần của rule 11: không label, vị trí, màu hay icon chưa được duyệt; gọi tên một chỗ bằng region | Requirement khóa chặt một design mà không ai chọn | Lint (banned words, interface words) + Review |
| FRG-10 | Tên file `FR-xxx.md` có ba chữ số, bằng `id` trong frontmatter. ID là duy nhất. ID mới đi sau ID cao nhất đang có hoặc đã xóa. ID bị bỏ được ghi ở section 1, không dùng lại | Một ID mang hai nghĩa | Lint (name, format) + CI (unique) |

## 3. Illustrations

**FRG-02: dùng lại cho cùng hành vi.**

> Fail: một FR "ignore a repeated status event", và một FR thứ hai cùng nghĩa cho repeated fee event.
> Pass: một FR "a carrier event already applied leaves the money state unchanged". Mọi block nhận carrier event đều cite nó.

**FRG-09: hành vi, không phải design.**

> Fail: "The Export button is greyed out when no period is closed."
> Pass: "The system does not accept an export request when no period is closed."
