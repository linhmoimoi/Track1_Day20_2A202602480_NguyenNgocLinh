# AI Support Log

## Phần AI hỗ trợ có thể xác minh

| Phần việc | Nội dung AI hỗ trợ | Căn cứ và giới hạn |
|---|---|---|
| Bản nháp lab đã có trong repo | Soạn nội dung các mục 00–06 và checklist Gate 5 cho dự án AI Customer Support Agent; đề xuất hệ metric theo ticket, 8 event, mapping event–metric và 4 tiêu chí nghiệm thu. | Nội dung có trong [Metrics Pack.md](./Metrics%20Pack.md); yêu cầu hoàn thiện repo của người học xác nhận đây là nội dung AI đã hỗ trợ. Repo không lưu đủ lịch sử để xác định ngày hoặc công cụ của bản nháp trước đó. |
| Phiên hợp nhất bản nộp | AI hợp nhất bản Metrics Pack, làm rõ điều kiện value, cập nhật README và chuẩn hóa log nộp. | Có thể đối chiếu với các tệp trong repo; không gán các thao tác này cho người học. |
| Phiên biên tập reflection | AI viết lại đoạn “Điều tôi mang về áp dụng cho dự án thật” và soạn phần reflection từ nội dung lab và yêu cầu của người học. | Đây là bản nháp lời kể, chưa xác minh cảm nhận hoặc việc người học tự thực hiện; cần người học đối chiếu trước khi nộp. |

## Điểm cần phân biệt và giả định

- `support_response_sent` là **core action**: nhân viên tuyến đầu đã rà soát và gửi phản hồi cuối cùng gắn với ticket. Event này tự nó chưa chứng minh ticket được giải quyết có giá trị.
- `qualified_ticket_resolution` là **event value theo định nghĩa đề xuất trong bài**: ticket đã resolved, phản hồi đạt QA, và trong cửa sổ quan sát không có reopen cũng không có recontact. Cửa sổ **7 ngày**, tiêu chuẩn QA, lịch ca và các nguồn tracking để nối ticket với review/recontact vẫn là **giả định cần xác nhận** trước khi dùng metric trong sản phẩm thật.
- AI đã đề xuất tên event theo hành vi/đối tượng, thời điểm ghi sau khi thao tác hoàn tất và tiêu chí chống ghi trùng khi retry hoặc reload. Đây là thiết kế tracking đề xuất, chưa phải bằng chứng hệ thống đã triển khai.
- Tệp `AI LOG.md` từng là mẫu minh họa nêu khả năng nhầm `support_response_sent` với value. Mẫu không chứng minh AI đã thực sự mắc lỗi đó trong một phiên cụ thể, nên log này không ghi nhận nó là lỗi đã xảy ra.

## Reflection cá nhân — bản nháp để người học xác nhận

Phần dưới được viết từ nội dung bài lab và yêu cầu đã trao đổi; người học cần đọc lại và chỉnh nếu khác trải nghiệm thực tế.

**AI đã giúp tôi ở đâu?**

AI giúp tôi hệ thống hóa các mục của Metrics Pack thành một mạch từ core action, cadence, hệ metric đến retention, product loop và tracking. Phần gợi ý tám event cùng tiêu chí nghiệm thu giúp tôi thấy rõ mỗi chỉ số cần sự kiện và dữ liệu nào để tính được, thay vì chỉ đặt tên metric rồi dừng lại.

**AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?**

Điểm tôi phải đọc kỹ trong bản nháp là cách viết điều kiện không mở lại hoặc không liên hệ lại: chữ “hoặc” có thể bị hiểu thành chỉ cần đạt một điều kiện. Tôi cũng không muốn lấy `support_response_sent` làm bằng chứng ticket đã tạo value, vì gửi được phản hồi chưa nói lên kết quả giải quyết. Log cũ chỉ nêu khả năng nhầm lẫn này như một ví dụ, nên tôi không coi đó là một lỗi AI đã xảy ra. Cửa sổ 7 ngày và tiêu chuẩn QA vẫn là giả định cần kiểm tra trong dự án thật.

**Tôi đã tự sửa hoặc quyết định lại điều gì?**

Tôi giữ core action là nhân viên tuyến đầu rà soát rồi gửi phản hồi cuối cùng theo từng ticket; value chỉ được tính khi ticket đạt `qualified_ticket_resolution`. Trong bản nộp, điều kiện value được viết rõ là không có cả reopen lẫn recontact trong cửa sổ theo dõi, và retention chỉ xét khi nhân viên có ticket tiếp theo để xử lý. Tôi cũng giữ các nguồn tracking và ngưỡng chất lượng ở trạng thái cần xác nhận, thay vì trình bày chúng như dữ liệu sản phẩm đã có.
