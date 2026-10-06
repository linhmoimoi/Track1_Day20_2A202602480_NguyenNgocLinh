# AI Support Log

## Phần AI hỗ trợ có thể xác minh

| Phần việc | Nội dung AI hỗ trợ | Căn cứ và giới hạn |
|---|---|---|
| Bản nháp lab đã có trong repo | Soạn nội dung các mục 00–06 và checklist Gate 5 cho dự án AI Customer Support Agent; đề xuất hệ metric theo ticket, 8 event, mapping event–metric và 4 tiêu chí nghiệm thu. | Nội dung có trong [Metrics Pack.md](./Metrics%20Pack.md); yêu cầu hoàn thiện repo của người học xác nhận đây là nội dung AI đã hỗ trợ. Repo không lưu đủ lịch sử để xác định ngày hoặc công cụ của bản nháp trước đó. |
| Phiên hoàn thiện repo hiện tại | AI hợp nhất bản Metrics Pack, làm rõ điều kiện value, cập nhật README và chuẩn hóa log nộp. | Có thể đối chiếu với các tệp trong repo sau phiên này; không gán các thao tác này cho người học. |

## Điểm cần phân biệt và giả định

- `support_response_sent` là **core action**: nhân viên tuyến đầu đã rà soát và gửi phản hồi cuối cùng gắn với ticket. Event này tự nó chưa chứng minh ticket được giải quyết có giá trị.
- `qualified_ticket_resolution` là **event value theo định nghĩa đề xuất trong bài**: ticket đã resolved, phản hồi đạt QA, và trong cửa sổ quan sát không có reopen cũng không có recontact. Cửa sổ **7 ngày**, tiêu chuẩn QA, lịch ca và các nguồn tracking để nối ticket với review/recontact vẫn là **giả định cần xác nhận** trước khi dùng metric trong sản phẩm thật.
- AI đã đề xuất tên event theo hành vi/đối tượng, thời điểm ghi sau khi thao tác hoàn tất và tiêu chí chống ghi trùng khi retry hoặc reload. Đây là thiết kế tracking đề xuất, chưa phải bằng chứng hệ thống đã triển khai.
- Tệp `AI LOG.md` từng là mẫu minh họa nêu khả năng nhầm `support_response_sent` với value. Mẫu không chứng minh AI đã thực sự mắc lỗi đó trong một phiên cụ thể, nên log này không ghi nhận nó là lỗi đã xảy ra.

## Reflection cá nhân — người học tự hoàn thành

Chỉ ghi trải nghiệm thật của bạn: AI đã hữu ích ở đâu, có đề xuất nào bạn thấy sai hoặc hời hợt, bạn đã tự kiểm tra/chỉnh sửa hay quyết định lại điều gì. Phần dưới để trống để bạn tự viết trước khi nộp.

**AI đã giúp tôi ở đâu?**


**AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?**


**Tôi đã tự sửa hoặc quyết định lại điều gì?**
