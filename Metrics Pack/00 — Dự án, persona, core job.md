# 00 — Phạm vi của tệp bạn

1. Dự án: AI Customer Support Agent giúp nhân viên chăm sóc khách hàng xử lý yêu cầu hỗ trợ.
2. Persona: Nhân viên chăm sóc khách hàng tuyến đầu trực tiếp tiếp nhận và xử lý yêu cầu.
3. Core job: “Tôi phải xử lý nhiều yêu cầu hỗ trợ cùng lúc, nên mất thời gian tìm thông tin để trả lời chính xác và khiến khách phải chờ lâu.”

# 01 — Core Action

## Bốn khái niệm trong use case

| Khái niệm | Áp dụng vào use case |
|---|---|
| Core job | Xử lý nhiều yêu cầu hỗ trợ cùng lúc, tìm thông tin để trả lời chính xác và giảm thời gian khách phải chờ. |
| Core action | Nhân viên rà soát/chỉnh sửa rồi gửi phản hồi cuối cùng, trực tiếp trả lời yêu cầu và gắn với ticket. |
| Core value | Nhân viên xử lý yêu cầu nhanh hơn với phản hồi chính xác, giúp khách nhận được hướng giải quyết. |
| Core value event | Ticket được giải quyết và không bị mở lại hoặc khách không phải liên hệ lại trong cửa sổ quan sát. |

## Core Action Card

| Thành phần | Câu trả lời |
|---|---|
| Target user | Nhân viên chăm sóc khách hàng tuyến đầu trực tiếp tiếp nhận và xử lý yêu cầu. |
| Core job | Xử lý nhiều yêu cầu hỗ trợ cùng lúc, tìm thông tin để trả lời chính xác và giảm thời gian khách phải chờ. |
| Core action | Rà soát/chỉnh sửa và gửi phản hồi cuối cùng gắn với ticket; phản hồi phải trực tiếp trả lời yêu cầu và dựa trên thông tin sẵn có. |
| Object | Ticket yêu cầu hỗ trợ và phản hồi cuối cùng gắn với ticket đó. |
| Preconditions | Có ticket cần xử lý, thông tin liên quan để đối chiếu và bản nháp AI hoặc nội dung phản hồi để nhân viên rà soát. |
| Completion rule | Phản hồi đã được nhân viên rà soát, trực tiếp trả lời yêu cầu theo thông tin sẵn có và gửi thành công, gắn với ticket. |
| Core value | Xử lý yêu cầu nhanh hơn mà vẫn giúp khách nhận phản hồi chính xác, có hướng giải quyết. |
| Evidence of value | Ticket được đánh dấu đã giải quyết và không bị mở lại/khách không liên hệ lại trong cửa sổ quan sát đã thống nhất. |
| Candidate event | `support_response_sent` — ghi nhận ticket, người gửi và trạng thái rà soát; event này ghi nhận hành vi, không tự chứng minh ticket có giá trị. |

## Tự kiểm 5 tiêu chí

| Tiêu chí | Kết quả | Giải thích |
|---|---|---|
| Gần core value | Đạt | Gửi phản hồi đã rà soát là bước trực tiếp đưa yêu cầu đến hướng giải quyết; chất lượng được xét qua tiêu chuẩn phản hồi và bằng chứng ticket. |
| Có thể lặp lại | Đạt | Nhân viên thực hiện hành vi này mỗi khi cần trả lời một yêu cầu hỗ trợ. |
| Có thể quan sát | Đạt | Có thể ghi nhận phản hồi gửi thành công cùng ticket và người gửi. |
| Có ý nghĩa | Đạt | Hành vi chỉ được tính khi phản hồi đã rà soát và trực tiếp trả lời yêu cầu, không chỉ vì có event gửi. |
| Có thể tác động | Đạt | Sản phẩm có thể hỗ trợ tìm thông tin và rà soát bản nháp để giúp nhân viên phản hồi nhanh, chính xác hơn. |

## Kết luận Gate 1

Core action có actor (nhân viên tuyến đầu), object (ticket/phản hồi gắn với ticket) và completion rule (phản hồi đã rà soát, trực tiếp trả lời yêu cầu và gửi thành công) cụ thể. Đạt **5/5 tiêu chí**. Đây không phải “mở app” hay “hỏi AI”: hành vi là hoàn tất và gửi phản hồi có căn cứ cho một yêu cầu cụ thể; output AI chỉ là bản nháp hỗ trợ.

**Giả định cần xác nhận:** Agent cho phép nhân viên xem/chỉnh sửa bản nháp và gửi phản hồi gắn với ticket; hệ thống có thể ghi nhận trạng thái giải quyết, mở lại hoặc liên hệ lại. Cửa sổ quan sát cho bằng chứng giá trị chưa được xác định trong workspace.

# 02 — Nature & cadence

**Giả định tối thiểu:** Use case là nhân viên tuyến đầu xử lý ticket đến bằng AI Customer Support Agent; nhân viên rà soát/chỉnh sửa bản nháp AI rồi gửi phản hồi cuối cùng. Workspace chưa mô tả luồng ticket, nguồn thông tin hay quy trình phê duyệt cụ thể.

## Action Nature Card

| Thành phần | Câu trả lời |
|---|---|
| Actor | Nhân viên chăm sóc khách hàng tuyến đầu thực hiện hành vi; ticket là đối tượng được xử lý, không phải actor. |
| Intent | Giải quyết yêu cầu trong ticket và giúp khách nhận phản hồi chính xác mà không phải chờ lâu. |
| Trigger | Ticket mới đến hoặc được đưa cho nhân viên xử lý; đây là sự kiện bên ngoài. AI tạo bản nháp sau đó chỉ hỗ trợ công việc, không tự kích hoạt core action. |
| Effort | Thay đổi theo ticket: nhân viên đọc yêu cầu, tìm/đối chiếu thông tin, rà soát và có thể chỉnh bản nháp trước khi gửi; không có dữ liệu để ước lượng thời lượng. |
| Value timing | Bản nháp AI chưa phải value. Khi nhân viên gửi phản hồi phù hợp, khách có thể nhận hướng giải quyết sớm hơn; ticket được xác nhận giải quyết và không cần liên hệ lại chỉ rõ sau đó. |
| State | Theo giả định, ticket lưu phản hồi cuối cùng, người gửi và trạng thái gửi; trạng thái giải quyết/mở lại có thể được cập nhật sau. |
| Dependency | Cần ticket có thể xử lý và thông tin liên quan để kiểm tra phản hồi. Việc chờ thêm thông tin hoặc phê duyệt có thể trì hoãn gửi; workspace chưa xác nhận các bước này có luôn cần hay không. |
| Repeat condition | Có một ticket mới cần nhân viên phản hồi; mỗi ticket cần xử lý tạo một lý do riêng để lặp lại hành vi. |

## Dạng hành vi

**Phản ứng theo sự kiện.** Hành vi bắt đầu khi có ticket đến/cần phản hồi và lặp theo từng ticket, không theo lịch cố định. Workspace chỉ xác nhận core action của một nhân viên trên một ticket; chưa có căn cứ rằng hành vi này luôn gồm một workflow nhiều bước của cả team.

## Kết luận cadence

“Đối với **nhân viên tuyến đầu xử lý ticket đến**, core action **rà soát/chỉnh sửa và gửi phản hồi cuối cùng gắn với ticket** thường xuất hiện **mỗi khi có một ticket cần phản hồi** vì **ticket là trigger bên ngoài tạo nhu cầu xử lý; bản nháp AI không thay thế hành vi gửi phản hồi của nhân viên**. Do đó, nhịp đo phù hợp là **theo từng ticket/lần xử lý** ở cấp **ticket**.”

## Hai câu hỏi

- **Vì sao action nhiều hơn không nhất thiết là value nhiều hơn?** Gửi nhiều phản hồi có thể phản ánh nhiều ticket hơn, nhưng cũng có thể gồm phản hồi sai/chưa giải quyết được yêu cầu; số lần gửi không xác nhận kết quả tốt.
- **Nhanh hơn có thể là tín hiệu tốt thế nào?** Nếu nhân viên tìm và kiểm tra thông tin nhanh hơn mà vẫn gửi phản hồi phù hợp, khách có thể được trợ giúp sớm hơn; tốc độ một mình chưa chứng minh chất lượng hay giải quyết thành công.

## Kết luận Gate 2

Kết luận cadence điền đủ nguyên mẫu; phần “vì” dựa trên trigger là ticket cần phản hồi và vai trò hỗ trợ của bản nháp AI. Nhịp **theo từng ticket ở cấp ticket** nhất quán với dạng **phản ứng theo sự kiện**. Gate 2 đạt. Quy trình lưu trạng thái và các phụ thuộc nêu trên là giả định cần xác nhận.
