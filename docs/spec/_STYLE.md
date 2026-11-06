# Spec writing rules

Áp dụng cho mọi file trong `docs/spec/`. Rule 5 và 7 áp dụng cho field `System` và `When` của use case. Rule 11 áp dụng cho toàn bộ use case.

**Why:** mỗi câu chỉ được có một nghĩa, để một system response trở thành một requirement test được. Từ ngữ hằng ngày làm được cả hai việc này.

## Language policy

Phần hướng dẫn (các file `_STYLE`, `_MERMAID`, `_CRITERIA`, comment trong `_TEMPLATE`) viết bằng tiếng Việt. Nội dung spec (field `User`, `System`, `When`, statement của FR/NFR/BR, glossary term, evidence tag, ID) viết bằng tiếng Anh, vì các rule wording bên dưới và lệnh kiểm tra dựa trên từ tiếng Anh => nếu viết tiếng Việt thì không grep được.

## Rules

| # | Rule | Don't write | Write |
|---|---|---|---|
| 1 | **One thing, one name.** Dùng đúng từ trong glossary. Không thay bằng từ đồng nghĩa. | "carrier balance" và "money held" cho cùng một thứ | "carrier balance" ở mọi chỗ |
| 2 | **Use plain words.** show, keep, use, start, end, before, after | display, maintain, initialize, terminate, prior, subsequent | "The system shows the carrier balance." |
| 3 | **No idioms or flowery phrases.** | "green-light", "seal the deal", "U-turn" | "agree", "end", "change its mind" |
| 4 | **No vague verbs.** Cấm: handle, manage, support, ensure, process, carry out, appropriate, properly, smoothly. | "The system handles errors smoothly." | "The system reports it could not read the file and keeps the last imported statement." |
| 5 | **No "can", "should", "might", "may" in a system response.** Ghi hệ thống làm gì. Chỉ dùng **"is allowed to"** cho quyền của user. | "The system can show a message." | "The system shows a message." |
| 6 | **Short, active sentences.** Mỗi câu một hành động. Citation `[BR-xxx]` không tính. | "A message is shown that the import has stopped and how many rows are done." | "The system shows a message that the import has stopped. The message states how many rows were read." |
| 7 | **Conditions go in the When field.** System response không có "if". Khi hành vi khác nhau theo step, mở đầu bằng label: "At S3:", "On re-import:". | "If the file is invalid, the system rejects it." | When: "The file does not match a known statement format [BR-?]." System: "State the reason." |
| 8 | **One action per line. At most 7 lines per field.** | Một ô 110 chữ | Mỗi thứ user quan sát được một dòng |
| 9 | **Minimal bold.** Bold một từ glossary ở lần dùng đầu tiên trong dòng. Tối đa 2 chỗ mỗi dòng. | Bold cả một cụm | "Show the **discrepancy**." |
| 10 | **Evidence on its own line.** Mỗi nhận định một tag. Không đặt giữa câu. | "…the carrier balance stays at the old value `[observed: …]`, and does not include the new transfer." | `- **Evidence:** [observed: ghn-dashboard (balance unchanged after a transfer)]` |
| 11 | **Intent and response, not interface.** Phía user nói user muốn gì. Phía system nói hệ thống báo gì, giữ gì, đổi gì hoặc tạo gì. Không bao giờ gọi tên widget, thao tác, vị trí, style hay label. Chỉ gọi tên một chỗ bằng region (xem Regions). Nếu một chi tiết interface mang theo requirement thì viết requirement đó ra. | "The user opens the menu and picks a carrier statement." "Open the discrepancy view in the bottom corner." "Show a card with a retry button." | "The user picks a carrier statement." "Open the discrepancy view. The open discrepancies stay unchanged." "Let the user retry the import." |

Rule 4 tới 7 giữ cho response test được. Rule 1 tới 3 và 6 giữ cho nó dễ đọc. Rule 11 giữ cho spec đúng khi design thay đổi.

## Evidence tags

Mỗi nhận định một tag. Key giữ tiếng Anh để grep được; nội dung nguồn viết bằng văn xuôi:

- `[observed: <source> (<what it shows>)]` — thấy trong transcript hoặc product
- `[inferred: <source>]` — suy ra từ các sự thật đã quan sát
- `[assumed]` hoặc `[assumed: <what>]` — chưa có bằng chứng

Trong một list (usage context, knowledge, …), dòng cuối có thể là một dòng `- **Evidence:** [assumed]` duy nhất. Dòng này tính cho mọi item phía trên không có dòng Evidence riêng.

## Regions

Region là một chỗ chứa một loại thông tin. Region được định nghĩa bằng thứ nó chứa, không bao giờ bằng vị trí hay hình dạng. Danh sách region là đóng; mỗi product khai báo region của mình trong glossary. Project hiện chưa có region nào được chốt.

Use case được nói một thứ được show, giữ hoặc đổi trong một region. Use case không được nói region đó bố trí ra sao hay đi tới bằng cách nào. Muốn thêm region thì thêm một dòng vào glossary và ghi nó chứa gì.

## Glossary

Dùng các từ này cho các thứ này. Thêm dòng khi cần một từ mới. Không thêm từ đồng nghĩa. Một từ không bao giờ gọi tên widget, thao tác, vị trí hay style. Bảng bắt đầu trống; mỗi project khai báo term của mình và bổ sung dần khi hiểu thêm.

| Term | Meaning |
|---|---|
| **account** | The user's identity for access and for keeping their own data |
| _(add a row)_ | _(describe the meaning, do not name a widget or position)_ |

## How to check

Chưa có tool, nên phần review làm việc này. Có hai nhóm kiểm tra.

**Wording.** Chạy trên field `System` và `When`, và trên `Situation and goal`. Mỗi chỗ match phải được sửa hoặc ghi lại lý do.

```
handle|manage|support|ensure|process|carry out|appropriate|properly|smoothly|can|could|should|might|may
```

**Interface (rule 11).** Chạy trên toàn bộ use case, trừ frontmatter, block được generate và dòng `Research link`. Mỗi chỗ match được viết lại thành intent hoặc response. Chỗ match không phải ngôn ngữ interface (ví dụ "right" trong "right-to-left text") thì ghi lại lý do.

```
button|click|tap|swipe|scroll|menu|dropdown|dialog|popup|tab|sidebar|toolbar|card|chip|icon|toggle|checkbox|screen|page|corner|above|below|left|right|label|input field
```

Sau đó áp dụng **swap test** cho mỗi câu: tưởng tượng cùng product đó với một interface khác, ví dụ chỉ dùng cảm ứng hoặc chỉ dùng giọng nói. Nếu câu vẫn đúng thì pass. Nếu không, câu đang mô tả interface và phải viết lại.
