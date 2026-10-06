## AI Support Log — mẫu minh họa

**MẪU MINH HỌA — cần người học xác nhận và chỉnh trước khi nộp**

**AI đã giúp tôi ở đâu?**  
AI gợi ý cách đặt tên event theo dạng `object_action` và tiêu chí nghiệm thu để kiểm tra event chỉ được ghi khi hành vi hoàn tất, không bị ghi trùng khi reload hoặc retry. Trong bài này, ví dụ event là `support_response_sent` cho nhân viên tuyến đầu gửi phản hồi cuối cùng của ticket sau khi rà soát/chỉnh sửa.

**AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?**  
Trong bản nháp, AI có thể xem `support_response_sent` như bằng chứng ticket đã được giải quyết. Điều đó chưa đủ: gửi phản hồi là core action, còn value được xác nhận bằng `qualified_ticket_resolution` theo tiêu chuẩn bài. Cửa sổ không reopen/recontact trong 7 ngày là giả định cần xác nhận, không phải benchmark.

**Tôi đã tự sửa hoặc quyết định lại điều gì?**  

[Người học tự ghi bằng lời của mình điều đã thực sự sửa hoặc quyết định.]