---
id: VIS-001
title: ""
updated: YYYY-MM-DD
---

<!-- Viết theo docs/spec/_STYLE.md. Gate: _CRITERIA.md.
     Vision nói product là gì, không phải decision log, danh sách feature hay scope (VG-01).
     Trước khi viết một block, hỏi: nó có còn đúng nếu scope, interface hay code thay đổi không? Nếu không, nó thuộc chỗ khác (_CRITERIA.md section 1).
     Mỗi sự thật viết đúng một lần (VG-06). Không giá trị rule hay chất lượng (VG-09). Không từ khen (VG-12).
     Phần chưa chốt được gì ghi "Not written yet. See Q-x." Không viết độn (VG-14).

     Các field chung cho mọi statement block:
       Statement: điều gì đúng. Thì hiện tại cho điều product là. "The product aims to..." cho một định hướng.
       Status: "confirmed" (đã quyết) hoặc "proposed" (đề xuất, chờ approve). Luôn có mặt.
       Source: chỉ khi "proposed" — đề xuất đến từ đâu và được suy ra từ cái gì.
       Spec implications: spec cấp dưới phải giữ gì hoặc không được giả định gì. Chỉ những gì suy ra trực tiếp từ statement. Bỏ field khi Status là "proposed".
       Updated date: chỉ một `updated` trong frontmatter, là ngày sửa gần nhất. Không ghi ai sửa; git history đã ghi. -->

## What the product is

<!-- Câu hỏi 1. Đây là loại product gì, và các ý cần để hiểu nó. Không phải danh sách feature.
     Một năng lực (import bảng kê, export dữ liệu, AI giải thích) là use case, trừ khi đã khẳng định nó định nghĩa product (VG-01).
     Fields: Statement, Status, Source, Spec implications. -->

### I-1 · short name

- **Statement:**
- **Status:** proposed
- **Source:**

## Why it exists

<!-- Câu hỏi 2 và 3. Vấn đề product giải quyết, cho ai, và giá trị chính nó mang lại.
     Chỉ viết những gì chủ product đã nói hoặc bằng chứng cho thấy. Không bịa vấn đề, kết quả research hay lợi ích.
     Chỉ có evidence [assumed] thì viết như một niềm tin: "I believe that...".
     Fields: Statement, Status, Source, Evidence, Spec implications. -->

### W-1 · short name

- **Statement:**
- **Status:** proposed
- **Source:**
- **Evidence:** [assumed]

## Principles

<!-- Câu hỏi 4. Các rule định hướng lựa chọn khi spec phải chọn. Mỗi rule loại bỏ một điều gì đó.
     Không phải giải pháp kỹ thuật: "the core reconciles without AI" là nguyên tắc; "put carrier events on a queue" là decision record (VG-02).
     Fields: Statement, Status, Source, Why, Spec implications. -->

### P-1 · short name

- **Statement:**
- **Status:** proposed
- **Source:**
- **Why:**

## Boundaries

<!-- Câu hỏi 5. Product KHÔNG phải là gì, theo bản chất. Kiểm tra: nếu có thời gian vô hạn, nó có còn đúng không? Nếu không, đó là scope (VG-03).
     Feature còn thiếu không phải boundary. Giới hạn của V1 không phải boundary.
     Khi được, nêu điều đúng theo dạng khẳng định, không chỉ nêu sự vắng mặt.
     Fields: Statement, Status, Source, Why, Spec implications. -->

### B-1 · short name

- **Statement:**
- **Status:** proposed
- **Source:**
- **Why:**

## Open questions

<!-- Mỗi câu hỏi đang chờ quyết một block (VG-04). Bỏ section này nếu trống.
     Các field cố định theo thứ tự: Question, Affects.
     Question: kết thúc bằng "?". Không block nào khác trả lời nó.
     Affects: các spec item cấp dưới đang chờ câu trả lời, bằng ID (ví dụ UC-001 S5), hoặc "none yet". -->

### Q-1 · short name

- **Question:**
- **Affects:** none yet

## Removed

<!-- ID đã xóa, mỗi ID một dòng ghi nội dung đã chuyển đi đâu (VG-05). Không dùng lại. Bỏ section này nếu trống. -->
