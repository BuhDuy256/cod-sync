# Build workflow

Tài liệu tham chiếu cho việc build use case, từ spec tới code chạy được. Mọi session bắt đầu build một UC đều đọc file này.

## Trigger and scope

Workflow bắt đầu khi user yêu cầu một build. Scope linh hoạt:

| User says | Scope |
|---|---|
| "Build UC-001" | Toàn bộ UC — mọi step và alternative |
| "Build the fetch flow from UC-001" | Step S1-S2, alternative A1-A3 |
| "Build just the link validation" | Chỉ FR-001 |
| "Build the error handling for fetch failure" | Chỉ alternative A3 |
| "Build UC-001 S1-S3 without save" | Step S1-S3, bỏ S6 và các alternative liên quan tới save |

Bước đầu tiên luôn là Phase 1, không bao giờ nhảy thẳng vào implementation. Scope quyết định FR/NFR nào được đưa vào research, testing và implementation.

### Scope definition

Mỗi build bắt đầu bằng việc khai báo scope trong folder plan:

- **Folder name:** `plans/UC-XXX-short-label/` (ví dụ `plans/UC-001-fetch-flow/`)
- **Scope fields** (có trong mọi plan template):
  - Use case: UC-XXX
  - Steps included: S1-S2 (hoặc "all")
  - Alternatives included: A1, A3 (hoặc "all")
  - FRs in scope: FR-001, FR-002
  - NFRs in scope: NFR-001

Build toàn bộ UC dùng `plans/UC-XXX/` với "all" cho step và alternative.

### Multiple builds for the same UC

Nhiều scope của cùng một UC có thể tồn tại song song:
- `plans/UC-001-fetch-flow/` — S1-S2
- `plans/UC-001-save-flow/` — S6 + A8, A11
- `plans/UC-001-audio-prep/` — S4-S5 + A6

Mỗi scope có flow tracker issue và ticket riêng.

## Resuming

Khi user nói "continue UC-XXX" (hoặc tên một build có scope), đọc flow tracker issue trên GitHub trước. Issue này cho biết phase nào đang chạy và ticket nào còn mở.

## Division of labor

Mỗi phase chia việc giữa user (phần suy nghĩ phải ở lại với người) và agent (phần việc tay chân). Agent đề xuất; không gate nào đóng cho tới khi user đã review, góp ý và approve. Cách chia này là có chủ đích: user giữ phần research và phần phán đoán, để người sở hữu hệ thống là người hiểu hệ thống.

| Phase | User owns (research + judgment) | Agent owns (legwork) |
|---|---|---|
| 0 — Domain discovery | **Research domain và viết note. Chọn use case.** | Tạo checklist câu hỏi và chỉ ra nguồn public — **không** trả lời câu hỏi hay đề xuất câu trả lời. |
| 1 — Research | **Research và trả lời câu hỏi. Viết decision record** (`Choice` / `Why`). | Tạo checklist câu hỏi và bảng options/tradeoff — **không** trả lời câu hỏi hay điền choice/rationale. |
| 2 — Testing plan | Review, góp ý, approve. | Đề xuất testing plan. |
| 3 — Implementation plan | Review, góp ý, approve. | Đề xuất các step theo thứ tự. |
| 4 — Tickets | Approve scope. | Viết các ticket flash-ready. |
| 5 — Execution | Review PR, quyết định merge. | Implementer viết code; agent review. |
| 6 — Verification | **Đánh giá theo acceptance criteria.** | Chạy test suite và báo kết quả. |

Bảng này là chuẩn. Các list "Decision authority" trong `AGENTS.md` nói _ai quyết định_; bảng này nói _ai làm việc_.

## Traceability

Mỗi build duy trì một spine artifact: **traceability matrix** (`plans/UC-XXX/traceability-matrix.md`, tạo từ `plans/_TEMPLATES/`). Mỗi FR/AC (và mỗi NFR) một dòng, nối `FR/AC → RQ/DEC → test → impl ticket → verification`.

**No-orphan rule:** mỗi deliverable phải có nơi dùng nó ở phía sau. Một deliverable không được dùng ở đâu cả là lỗi, không phải trung tính. Cụ thể:

- Mọi FR/AC và NFR trong scope có một dòng trong matrix.
- Mọi FR/AC và NFR trong scope có ít nhất một test (sau Phase 2).
- Mọi decision (DEC) được ít nhất một test hoặc implementation step dùng tới.
- Mọi research question (RQ) đã trả lời dẫn tới một DEC hoặc một dòng dùng kết quả của nó.
- Mọi test và implementation ticket map ngược về một dòng trong matrix.

Matrix được tạo sẵn các dòng ở Phase 1 (mỗi FR/AC/NFR trong scope một dòng) và điền dần khi mỗi phase tạo ra link của nó. **Không gate nào được đóng khi matrix còn orphan mà phase đó phải giải quyết.** Điều kiện này được thêm vào mọi gate bên dưới.

## Document rules

Mọi plan document được tạo ra (và các template trong `plans/_TEMPLATES/`) theo sáu rule. Rule 5 và rule 6 áp dụng cho mọi document trong repo. Các rule phục vụ hai người đọc cùng lúc: người lướt qua file, và agent đọc lại file ở mỗi phase và trả token cho từng dòng. Rule giống nhau cho cả hai vì cách sửa giống nhau: đưa phần quan trọng lên đầu, và không bao giờ nói một điều hai lần.

1. **Front-load.** File mở đầu bằng block `## At a glance`: scope, trạng thái hiện tại, và link tới artifact quan trọng nhất (thường là matrix). Block này là toàn bộ phần tóm tắt, phần bên dưới không bắt buộc đọc. Người đọc xong block là dừng; agent đọc xong block và chỉ đọc sâu hơn khi task cần.
2. **Link, don't restate.** Mỗi sự thật chỉ có một chỗ ở. Testing plan, implementation plan hay flow tracker nhắc tới một dòng matrix (bằng ID FR/AC và link), không chép lại nội dung requirement. Trùng lặp là chỗ tốn token nhất và khó đọc nhất (người đọc không biết bản nào là bản chuẩn). Matrix là chỗ ở của spine FR/AC → test → impl.
3. **Fixed section order.** Mỗi template cố định thứ tự heading và generator giữ đúng thứ tự đó. Anchor dự đoán được giúp người đọc (người hoặc agent) nhảy thẳng tới một section, ví dụ một gate hay một bảng, thay vì đọc cả file.
4. **Length budget.** Mỗi document dài không quá khoảng một trang. Nếu dài hơn thì tách file hoặc link ra ngoài, thay vì viết thêm vào. Giới hạn độ dài là thứ buộc rule 2 được tuân thủ.
5. **State content, not provenance.** Document nói nó chứa gì và dùng để làm gì. Document không nói ai viết, ai trả lời hay ai quyết định. Vai trò chỉ nằm ở "Division of labor"; link tới đó khi người đọc cần. Git đã ghi lại tác giả.
6. **One line per paragraph.** Mỗi đoạn văn hoặc mỗi list item nằm trên đúng một dòng; không tự xuống dòng giữa câu, editor sẽ tự soft-wrap. Ngoại lệ: code block, bảng, và các dòng metadata (`**Ticket:**`, `**Use case:**`, ...) mỗi field một dòng.

## Phases

### Phase 0 — Domain discovery

**Goal:** hiểu domain đủ để chọn use case có lý do, không phải đoán. Chạy một lần cho mỗi product (và chạy lại khi mở ra một mảng domain mới), trước mọi UC build. Phase này nằm trước các build phase: Phase 1 trả lời các ẩn số kỹ thuật cho một use case đã có; Phase 0 quyết định use case nào nên có.

**Input:** brief (`docs/spec/00-brief/`) và vision (`docs/spec/01-product-vision/`).

**Process:**

1. Agent duy trì domain checklist ở `docs/research/domain/README.md` (các mảng, spec item mà mỗi mảng mở khóa, nguồn để bắt đầu) và mở một GitHub Issue cho mỗi mảng, label `phase:domain`. Issue chứa các câu hỏi đánh số của mảng dưới dạng task list; câu hỏi chỉ nằm ở đó.
2. **User research và viết một note cho mỗi mảng** trong `docs/research/domain/`, theo `docs/research/_STYLE.md` (vấn đề → đã thử gì → quan sát được gì → ý nghĩa). Một câu hỏi được đóng khi đã trả lời trong note, hoặc khi được đánh dấu out of scope kèm lý do một dòng, rồi tick trong issue. Cột Status của mảng trong checklist được cập nhật, và issue được đóng khi mọi câu hỏi đã tick.
3. Mỗi note hoàn chỉnh đưa dữ liệu vào spec: một dòng glossary trong `docs/spec/_STYLE.md`, một giá trị business rule, một loại chênh lệch kèm nguồn, `Evidence` mạnh hơn cho một vision block `W-x`, hoặc một use case ứng viên. Ai quyết định: `AGENTS.md` "Decision authority".
4. User chọn các use case và build đầu tiên từ các note. Mỗi use case link tới note sinh ra nó trong section `Product evidence`.

**Gate:** user giải thích được COD cash flow và danh mục chênh lệch bằng lời của mình; mọi câu hỏi trong checklist đã được trả lời hoặc đánh dấu out of scope; mọi use case được chọn link tới ít nhất một domain note (không có use case nào thiếu lý do).

### Phase 1 — Research

**Goal:** trả lời mọi ẩn số kỹ thuật trước khi lên plan.

**Input:** file UC, các FR, NFR, BR của nó.

**Process:**

1. Chạy skill `research-questions` trên UC để tạo research checklist.
2. Tạo checklist ở `plans/UC-XXX/research-checklist.md`.
3. Tạo traceability matrix ở `plans/UC-XXX/traceability-matrix.md` từ `plans/_TEMPLATES/traceability-matrix.md`, mỗi FR/AC và NFR trong scope một dòng.
4. Tạo GitHub Issue cho mỗi câu hỏi bằng template `research-ticket`. Label: `phase:research`, `uc:XXX`.
5. Với câu hỏi kỹ thuật, agent đưa ra các option kèm bảng tradeoff. Bảng chỉ liệt kê lựa chọn, không trả lời câu hỏi.
6. **User research và viết câu trả lời.** Mỗi câu hỏi đã trả lời tạo ra một trong hai:
   - Cập nhật file research trong `docs/research/`, hoặc
   - Decision record trong `docs/decisions/DEC-NNN-topic.md`, user điền `Choice` và `Why` bằng lời của mình.
7. Đóng mỗi research ticket khi câu hỏi đã được trả lời hoặc quyết định, và ghi link RQ/DEC vào (các) dòng matrix mà nó phục vụ.

**Gate:** mọi research ticket của UC đã đóng; matrix đã có dòng cho mỗi FR/AC/NFR trong scope; mọi RQ đã trả lời dẫn tới một DEC hoặc một dòng dùng kết quả của nó (không có research orphan).

### Phase 2 — Testing plan

**Goal:** định nghĩa mọi test trước khi viết bất kỳ dòng implementation nào.

**Input:** các FR kèm AC, NFR, decision từ Phase 1.

**Process:**

1. Chạy skill `testing-plan` trên FR/AC và decision của UC.
2. Tạo plan ở `plans/UC-XXX/testing-plan.md`.
3. Tạo GitHub Issue cho các test stub trước implementation bằng template `test-stub-ticket`. Label: `phase:test-stubs`, `uc:XXX`.
4. Các loại test và phase của chúng:

   | Type | When written | Phase label |
   |---|---|---|
   | Acceptance tests | Trước implementation | `phase:test-stubs` |
   | Security tests | Trước implementation | `phase:test-stubs` |
   | Unit tests | Gộp vào implementation ticket | `phase:impl` |
   | Integration tests | Sau các module mà nó test | `phase:post-impl` |
   | E2E tests | Sau toàn bộ implementation | `phase:post-impl` |
   | Smoke tests | Sau toàn bộ implementation | `phase:post-impl` |
   | Recovery / resilience tests | Sau các module mà nó test | `phase:post-impl` |
   | Regression tests | Tăng dần theo các bug fix | `phase:post-impl` |
   | Performance tests | Sau implementation, khi có NFR | `phase:post-impl` |

5. Đóng mỗi test stub ticket khi file test đã tồn tại và stub chạy được (red).
6. Ghi mỗi test ticket vào dòng matrix của nó, và ghi DEC mà mỗi test phụ thuộc.

**Gate:** mọi ticket `phase:test-stubs` của UC đã đóng; mọi dòng matrix có ít nhất một test; mọi DEC trong scope được ít nhất một test dùng tới (không có requirement chưa test, không có decision orphan).

### Phase 3 — Implementation plan

**Goal:** tạo danh sách các implementation step theo thứ tự, gắn với test.

**Input:** testing plan, decision, câu trả lời research.

**Process:**

1. Tạo plan ở `plans/UC-XXX/implementation-plan.md`.
2. Mỗi step ghi rõ:
   - Build gì (module, function, đường dẫn file).
   - Làm cho test nào pass.
   - Phụ thuộc decision nào.
3. User review và approve plan.

**Gate:** user approve implementation plan; mọi dòng matrix có ít nhất một implementation step (không có requirement nào bị bỏ sót).

### Phase 4 — Implementation tickets

**Goal:** chia plan thành các GitHub Issue phù hợp với flash model.

**Input:** implementation plan đã được approve.

**Process:**

1. Tạo GitHub Issue bằng template `implementation-ticket`. Label: `phase:impl`, `uc:XXX`.
2. Mỗi ticket có:
   - `Blocked by` trỏ tới các ticket tiên quyết (test stub, module khác).
   - Một test command làm acceptance criteria.
   - Ranh giới `Do NOT` rõ ràng.
3. Tạo post-implementation test ticket bằng template `post-impl-test-ticket`. Label: `phase:post-impl`, `uc:XXX`. Các ticket này bị block bởi implementation ticket mà chúng phụ thuộc.
4. Cập nhật flow tracker issue với mọi số ticket.
5. Điền cột Test và Impl của matrix bằng link ticket.

**Gate:** mọi ticket đã được tạo và link; cột Test/Impl của matrix đã điền; không có test hay implementation ticket nào thiếu dòng matrix (không có ticket orphan).

### Phase 5 — Execution and review

**Goal:** implement mọi ticket và pass mọi test.

**Input:** các ticket theo thứ tự phụ thuộc.

**Process:**

1. User giao ticket cho implementer (DeepSeek/GLM Flash qua tool bên ngoài, hoặc Claude sub-agent).
2. Mỗi implementer:
   - Đọc ticket và context được link.
   - Push một branch chứa implementation.
   - Chạy test command trong ticket để tự kiểm tra.
3. Claude review mỗi PR bằng `/code-review`.
4. Merge khi test pass và review approve.
5. Đóng ticket.
6. Cập nhật flow tracker issue.

**Gate:** mọi ticket `phase:impl` và `phase:post-impl` đã đóng.

### Phase 6 — Verification

**Goal:** xác nhận UC chạy đúng từ đầu tới cuối.

**Input:** mọi code đã merge, mọi test xanh.

**Process:**

1. Chạy toàn bộ test suite.
2. Chạy smoke test.
3. Chạy E2E test cho happy path và các alternative flow của UC.
4. Chạy resilience test cho các alternative lỗi của UC.
5. Đối chiếu với acceptance criteria của UC **từng dòng trên matrix**, tick cột Verified cho mỗi AC đã xác nhận trên code thật. Đây là phần đánh giá của user (xem "Division of labor").
6. Đóng flow tracker issue.

**Gate:** flow tracker issue đã đóng; cột Verified của mọi dòng matrix đã tick (mọi AC đã verify end-to-end). UC hoàn tất.

## Flow tracker issue

Mỗi build có scope có một flow tracker issue, là issue gốc. Issue được tạo khi bắt đầu Phase 1 và link tới mọi ticket khác. Phần khai báo scope nằm ở đầu. Template: `.github/ISSUE_TEMPLATE/flow-tracker.md`.

Tracker dùng format sau (file local dùng link đầy đủ theo "Linking convention"; body của GitHub issue dùng `#N` trần vì GitHub tự link):

```markdown
## Phase 1: Research
- [ ] [#N]({base}/issues/N) question-title (status)

## Phase 2: Testing Plan
- [ ] [#N]({base}/issues/N) test-stub-title
Blocked by: Phase 1 complete

## Phase 3: Implementation Plan
- [ ] [#N]({base}/issues/N) plan-review
Blocked by: Phase 2 complete

## Phase 4: Implementation
- [ ] [#N]({base}/issues/N) module-title
Blocked by: [#test-stub]({base}/issues/N), [#other-module]({base}/issues/N)

## Phase 5: Post-impl Testing
- [ ] [#N]({base}/issues/N) test-title
Blocked by: [#module]({base}/issues/N)

## Phase 6: Verification
Blocked by: Phase 5 complete
```

## Ticket rules for flash models

Flash model (DeepSeek V4.1 Flash, GLM 5.3 Flash) cần ticket có ít bước suy luận nhất có thể. Mọi implementation ticket phải theo các rule sau:

1. **One concern per ticket.** Một function, một component, một module.
2. **Exact file paths.** Không viết "tạo một validation module" mà viết "tạo `src/domain/source-validator.ts`".
3. **Input/output contract.** Function signature, kiểu tham số, kiểu trả về.
4. **Test command.** Command chứng minh ticket đã xong.
5. **Do NOT section.** Ranh giới rõ ràng: những gì KHÔNG được đụng, refactor hay thay đổi.
6. **Blocked by.** Các ticket tiên quyết phải được merge trước khi bắt đầu.
7. **Context section.** Những gì đã có mà implementer cần biết. Ghi đường dẫn file và mô tả ngắn, không viết "xem codebase".
8. **Maximum 3 files changed per ticket.** Nếu cần sửa nhiều file hơn thì tách ticket.

## Labels

| Label | Meaning |
|---|---|
| `uc:XXX` | Ticket thuộc use case nào |
| `phase:research` | Ticket Phase 1 |
| `phase:test-stubs` | Ticket Phase 2 |
| `phase:impl-plan` | Ticket Phase 3 |
| `phase:impl` | Implementation ticket Phase 4 |
| `phase:post-impl` | Post-implementation test ticket Phase 5 |
| `flow-tracker` | Tracker issue gốc của một UC |
| `flash-ready` | Ticket phù hợp cho implementer là flash model |

## Milestones

Mỗi UC build một milestone: `UC-XXX`. Mọi ticket của UC đó thuộc milestone này.

## Linking convention

Mọi tham chiếu chéo giữa file, issue và deliverable phải là link Markdown bấm được, không bao giờ là `#N` trần hay đường dẫn file thuần. Áp dụng cho mọi output: plan file, issue body, research file, decision file và các lần cập nhật flow tracker.

Lấy base URL của repo từ `git remote get-url origin` khi bắt đầu mỗi build.

| Reference type | Format |
|---|---|
| Issue from a local file | `[#N](https://github.com/{owner}/{repo}/issues/N)` |
| File from an issue body | `[docs/research/topic.md](https://github.com/{owner}/{repo}/blob/main/docs/research/topic.md)` |
| Issue from an issue body | `#N` (GitHub tự link; không cần đổi) |
| Blocked-by in a local file | `[#N](https://github.com/{owner}/{repo}/issues/N)` |

**Where to apply:**

- **Research checklist** — cột Ticket, cột File của Deliverable map
- **Flow tracker** (bản local trong `plans/`) — mọi tham chiếu `#N`
- **Research files** (`docs/research/`) — field `**Ticket:**` và `**Blocked by:**`
- **Decision files** (`docs/decisions/`) — các tham chiếu `ticket #N`
- **Issue bodies** — section Deliverable (link tới file), tham chiếu Flow tracker (tự link)
