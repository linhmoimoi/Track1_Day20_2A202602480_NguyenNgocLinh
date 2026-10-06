# Track1 Day20 — 2A202602480 — Nguyễn Ngọc Linh

- **Họ tên:** Nguyễn Ngọc Linh
- **MHV:** 2A202602480
- **Tên repo:** `Track1_Day20_2A202602480_NguyenNgocLinh`
- **Dự án chọn làm:** AI Customer Support Agent giúp nhân viên chăm sóc khách hàng xử lý yêu cầu hỗ trợ
- **Bản nộp Metrics Pack:** [Metrics Pack.md](./Metrics%20Pack.md)
- **AI Support Log:** [ai-support-log.md](./ai-support-log.md)

## Cấu trúc repo

```text
Track1_Day20_2A202602480_NguyenNgocLinh/
├── README.md
├── Metrics Pack.md
└── ai-support-log.md
```

## Điều tôi mang về áp dụng cho dự án thật
Điều tôi muốn áp dụng là tách việc gửi phản hồi khỏi kết quả giải quyết ticket. `support_response_sent` cho biết nhân viên đã hoàn tất một bước xử lý, còn `qualified_ticket_resolution` mới thể hiện ticket đạt tiêu chuẩn giá trị đã định nghĩa trong bài. Khi đánh giá dự án thật, tôi sẽ đọc số ticket đạt chuẩn cùng tỷ lệ khách liên hệ lại hoặc ticket bị mở lại, để việc phản hồi nhanh hơn không che khuất vấn đề chất lượng. Trước khi dùng các chỉ số này để kết luận, tôi cần xác nhận tiêu chí QA, cửa sổ theo dõi 7 ngày và nguồn dữ liệu nối các lần liên hệ với ticket.
