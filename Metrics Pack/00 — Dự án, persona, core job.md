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

# 03 — Metric System

**Phạm vi:** Nhân viên tuyến đầu xử lý ticket đến bằng AI Customer Support Agent; core action là gửi phản hồi cuối cùng sau khi rà soát/chỉnh sửa bản nháp. Các event, cửa sổ và ngưỡng vận hành dưới đây là **đề xuất cần xác nhận** vì workspace chưa có SLA, dữ liệu ticket hay quy tắc QA.

## Activation

| Thành phần | Định nghĩa đề xuất |
|---|---|
| Start event | `actionable_ticket_assigned`: lần đầu nhân viên được giao một ticket đến cần phản hồi. Đây là lúc bắt đầu hành trình use case, không phải login/mở app. |
| Activation event | `support_response_sent` đầu tiên: nhân viên đã rà soát/chỉnh sửa, gửi phản hồi trực tiếp trả lời ticket và phản hồi được lưu thành công. Đây là first core action; tự nó chưa chứng minh ticket có giá trị. |
| Time window | Từ lúc start event đến hết ca làm việc đầu tiên của nhân viên. Đây là ngưỡng vận hành tạm tính, không phải SLA hay benchmark; cần xác nhận với lịch xử lý thực tế. |
| Value confirmation | `qualified_ticket_resolution`: ticket được đánh dấu giải quyết, phản hồi đạt tiêu chuẩn chất lượng bên dưới và không bị mở lại/khách không liên hệ lại trong 7 ngày lịch sau khi giải quyết. Vì cần chờ kết quả và cửa sổ theo dõi, đây là xác nhận trễ; 7 ngày là giả định cần kiểm tra, không phải benchmark. |

## Engagement — góc đo Breadth

| Góc đo | Định nghĩa | Vì sao phù hợp |
|---|---|---|
| Breadth | Trong một cohort ticket được giao, tỷ lệ ticket đến cần phản hồi của nhân viên có `support_response_sent` sau rà soát: số ticket đủ điều kiện có phản hồi gửi thành công / tổng ticket đủ điều kiện được giao. Đếm ticket duy nhất, không đếm số lần sửa/gửi lại. | Ticket là đơn vị phát sinh nhu cầu tự nhiên ở mục 02. Đo độ phủ theo ticket tránh ép nhịp daily/weekly; độ phủ cao hơn chưa chắc tốt nếu chất lượng ticket giải quyết giảm. |

## North Star Metric

**NSM đề xuất:** Số **ticket duy nhất được giải quyết đạt tiêu chuẩn chất lượng trên mỗi nhân viên tuyến đầu, tính khi từng ticket hoàn tất vòng đời xử lý tự nhiên** (tổng hợp qua cohort ticket đến; không áp lịch ngày/tuần làm cadence chính).

**Công thức:** `COUNT(DISTINCT ticket_id)` thỏa đồng thời: (1) nhân viên đã gửi phản hồi cuối cùng sau rà soát, trực tiếp trả lời yêu cầu và dựa trên thông tin sẵn có; (2) ticket được đánh dấu đã giải quyết; (3) kiểm tra QA xác nhận phản hồi liên quan và có căn cứ; (4) ticket không bị mở lại hoặc khách không liên hệ lại trong 7 ngày lịch sau khi giải quyết.

- **Unit of value:** một ticket được giải quyết có chất lượng.
- **Quality threshold:** đủ bốn điều kiện trên; tiêu chuẩn QA và cửa sổ 7 ngày là đề xuất cần xác nhận, không phải dữ kiện/benchmark đã biết.
- **Frequency:** ghi nhận một lần khi kết thúc vòng đời ticket và hết cửa sổ xác nhận; báo cáo theo cohort ticket đến để giữ đúng nhịp theo từng ticket.
- **Vì sao phản ánh value:** đo yêu cầu khách được giải quyết ổn định, không phải lượt hỏi AI hay số phản hồi đã gửi.

## Leading indicators

| Chỉ báo đề xuất | Vì sao có cơ sở dự báo action/value lặp lại |
|---|---|
| Tỷ lệ ticket được giao có bản nháp AI được nhân viên đánh giá là liên quan và có căn cứ để rà soát. | Bản nháp phù hợp có thể giảm thời gian tìm/soạn thông tin, giúp nhân viên tiến tới core action; cần định nghĩa cách ghi nhận đánh giá, không coi output AI tự thân là value. |
| Thời gian từ lúc giao ticket đến khi gửi phản hồi đã rà soát, xem theo ticket. | Nếu thời gian giảm mà chất lượng giữ ổn định, có cơ sở cho thấy trở ngại tìm và kiểm tra thông tin giảm, giúp nhiều ticket được xử lý kịp hơn; tốc độ riêng lẻ không xác nhận value. |

## Counter-metric

| Chỉ số bảo vệ | Định nghĩa | Hướng xấu |
|---|---|---|
| Tỷ lệ ticket bị mở lại hoặc khách liên hệ lại trong 7 ngày | Số ticket đã đánh dấu giải quyết nhưng bị mở lại/khách liên hệ lại trong cửa sổ 7 ngày / tổng ticket đánh dấu giải quyết đã đủ 7 ngày theo dõi. Cửa sổ là giả định cần xác nhận. | Tăng lên; có thể cho thấy NSM tăng nhờ đóng ticket nhanh nhưng phản hồi chưa giải quyết đúng nhu cầu. |


# 04 — Retention Definition

**Định nghĩa đề xuất theo cơ hội ticket:** đo nhân viên tuyến đầu (actor ở mục 01), và chỉ xác định retention khi có cơ hội ticket tiếp theo; không xem thiếu ticket được giao là churn.

| Thành phần | Câu trả lời |
|---|---|
| Unit | Nhân viên chăm sóc khách hàng tuyến đầu (user cá nhân). Actor thực hiện core action là nhân viên; ticket là object. Dùng định danh nhân viên ổn định để nối các ticket của cùng người. |
| Cohort entry | `actionable_ticket_assigned` đầu tiên cho nhân viên trong use case; ticket cần phản hồi và được tính là cơ hội xử lý đầu tiên. |
| Return event | `qualified_ticket_resolution` trên một ticket khác được giao sau cohort entry: phản hồi cuối cùng đã rà soát được gửi, ticket được giải quyết và đạt cùng tiêu chuẩn chất lượng ở mục 03. |
| Window | Custom, theo cơ hội và vòng đời ticket: sau cohort entry, chờ đến khi có ticket đủ điều kiện tiếp theo; cửa sổ return của ticket đó kéo từ lúc được giao đến khi giải quyết và hết 7 ngày lịch xác nhận. Nếu chưa có ticket tiếp theo thì retention chưa quan sát được. 7 ngày là giả định cần xác nhận. |
| Threshold | Ít nhất 1 ticket tiếp theo đạt `qualified_ticket_resolution` trong cửa sổ trên để tính retained. Chỉ đưa vào mẫu số những nhân viên có ticket tiếp theo đủ điều kiện; báo cáo riêng số người chưa có cơ hội return. |
| Segment | Nhân viên tuyến đầu dùng AI Customer Support Agent để xử lý ticket đến và được giao ticket cần phản hồi; không gộp vai trò hay use case khác. |

### Diễn giải retention theo ba mốc của lab

- **Natural cycle:** đọc retention theo cơ hội ticket tiếp theo và vòng đời xử lý đến khi hoàn tất cửa sổ chất lượng; không gán D7 hay tuần cố định. Thời gian chờ ticket tiếp theo cần được giữ riêng, không tính là thất bại return.
- **Cohort đúng segment:** so sánh cùng nhóm nhân viên tuyến đầu, cùng use case ticket đến và có cơ hội được giao ticket tiếp theo; tránh trộn nhóm không có cơ hội hành động.
- **Benchmark category:** chỉ đối chiếu với benchmark có nguồn xác thực và cùng loại quy trình hỗ trợ, segment, event, ngưỡng chất lượng và cách xử lý cửa sổ; workspace chưa có nguồn nên không đặt con số benchmark.

## Tự kiểm Gate 3

| Điều kiện | Kết quả | Căn cứ |
|---|---|---|
| Activation có start event, activation event và time window | Đạt | Có ticket được giao làm start, phản hồi đầu tiên đã rà soát được gửi làm activation, và ngưỡng tạm tính là hết ca làm đầu tiên; ngưỡng cần xác nhận. |
| Retention đủ sáu thành phần và khớp cadence mục 02 | Đạt | Đủ unit, cohort entry, return event, window, threshold, segment; return dựa trên ticket tiếp theo và value event theo nhịp từng ticket. |
| NSM có unit of value, quality threshold và frequency | Đạt | Đếm ticket giải quyết đạt điều kiện QA/outcome, mỗi ticket một lần khi hết vòng đời và cửa sổ xác nhận. |
| Có ít nhất một counter-metric | Đạt | Tỷ lệ reopen/liên hệ lại bảo vệ chất lượng khi số ticket giải quyết tăng. |

**Gate 3 đạt.** Các định nghĩa đủ cấu phần và nhất quán với cadence theo ticket. Cửa sổ activation một ca, QA và cửa sổ 7 ngày là giả định vận hành cần xác nhận bằng quy trình/dữ liệu thực tế; không có benchmark số nào được khẳng định.
