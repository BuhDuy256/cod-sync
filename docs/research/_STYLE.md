# Research notes — style guide

Đọc file này trước khi viết hoặc sửa bất kỳ file nào trong `docs/research/`. Đọc luôn các note đã có trong file đích để giữ cùng giọng văn trước khi viết thêm.

## Structure

1. Dùng numbered list làm cấu trúc chính. Mỗi số trình bày một ý hoặc một câu hỏi. Đánh số tiếp theo số đang có trong file.

2. Dùng bullet bên trong một mục khi cần liệt kê chi tiết. Chỉ dùng bảng khi so sánh nhiều thứ theo cùng tiêu chí (ví dụ kết quả trên nhiều URL). Dùng code block cho command hoặc đoạn response ngắn.

3. Không dùng bold, italic hay sub-heading trong văn bản thường. Giữ nguyên heading và metadata đã có. Dùng inline code cho URL, command, tên file, header hoặc giá trị kỹ thuật.

4. Mỗi đoạn văn hoặc mỗi list item nằm trên đúng 1 dòng. Không tự xuống dòng giữa câu, editor sẽ tự soft-wrap. Ngoại lệ: code block, bảng, các dòng metadata (`**Ticket:**`, `**Blocked by:**`, ...) mỗi field một dòng.

## Language

5. Viết câu tiếng Việt rõ, ngắn, trực tiếp. Giữ nguyên thuật ngữ kỹ thuật tiếng Anh quen thuộc (request, response, headers, fetch, backend, hosting, retry, ...), ID (FR, AC, UC, DEC) và tên field.

6. Khi đưa ra một thuật ngữ mới, giải thích ngay bằng hành vi cụ thể. Ví dụ: "Retry là gửi lại request sau khi bị lỗi." Tránh câu mơ hồ kiểu "xử lý phù hợp" hay "đảm bảo hoạt động ổn định".

## Reasoning

7. Giải thích theo thứ tự: vấn đề cần kiểm tra → đã thử gì → quan sát được gì → điều đó có ý nghĩa gì cho project.

8. Dùng một câu hỏi ngắn để dẫn vào điều cần hiểu, khi phù hợp. Ví dụ: "HTTP 200 có nghĩa là đã fetch được chương truyện không?" — rồi giải thích ngay sau đó.

9. Dùng `=>` để nối một quan sát với lời giải thích, hệ quả hoặc kết luận của nó. Chỉ dùng khi quan hệ rõ ràng, không đặt sau mọi câu.

10. Gắn bằng chứng với nhận định trong cùng một mục. Phân biệt rõ:
    - Observation: sự thật đo được (status, header, response body).
    - Inference: kết quả đó có thể cho thấy điều gì.
    - Proposal: project nên làm gì dựa trên kết quả.

11. Giữ cách diễn đạt gần với các note đã có, nhưng sửa thuật ngữ nếu nó sai về kỹ thuật. Không chép lại một nhận định thiếu chính xác chỉ để khớp văn phong.

12. Mỗi nguồn dùng trong note có URL chính xác và ngày đọc, đặt trong cùng mục với nhận định mà nó hỗ trợ.
