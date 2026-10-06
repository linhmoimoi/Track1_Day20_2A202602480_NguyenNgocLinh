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

# 05 — Product Loop

**Giả định cần xác nhận:** ticket mới được giao bên ngoài Agent; Agent có thể tạo bản nháp; hệ thống ticket lưu phản hồi và trạng thái xử lý. Workspace chưa xác nhận các khả năng này hoặc việc lưu lịch sử làm AI tốt hơn. Bản nháp AI là output hỗ trợ, không tự nó là value.

## Hai chu kỳ liên tiếp

| Bước | Chu kỳ 1 | Chu kỳ 2 |
|---|---|---|
| Natural trigger | Một ticket đến cần phản hồi được giao cho nhân viên. | Một ticket đến khác cần phản hồi được giao sau đó; đây là trigger mới từ công việc bên ngoài. |
| Core action | Nhân viên rà soát/chỉnh sửa bản nháp rồi gửi phản hồi cuối cùng, trực tiếp trả lời ticket. | Nhân viên lặp lại hành vi đó trên ticket mới. |
| Immediate value | Khách nhận phản hồi có hướng giải quyết sớm hơn; value chỉ được xác nhận khi `qualified_ticket_resolution` đạt tiêu chuẩn Phase 3. | Ticket thứ hai cũng chỉ tạo repeat value sau khi đạt cùng tiêu chuẩn chất lượng và cửa sổ xác nhận. |
| Saved state / investment | **Theo giả định:** phản hồi, người gửi và trạng thái được lưu trong lịch sử ticket để tiếp tục xử lý ticket đó; không giả định dữ liệu này tự cải thiện AI. | **Theo giả định:** lịch sử của ticket thứ hai được lưu tương tự; nhân viên vẫn cần một ticket mới để có lý do hành động tiếp. |
| Next natural trigger | Ticket đến tiếp theo cần phản hồi; trigger không phụ thuộc việc mở dashboard hay nhận notification. | Ticket mới tiếp theo tiếp tục mở ra cơ hội xử lý theo cùng cơ chế. |

## Loại loop

**Event-response.** Core action xuất hiện để phản ứng với ticket đến và lặp theo từng ticket, khớp dạng hành vi và cadence theo ticket ở mục 02; không phải thói quen theo lịch cố định.

## Nếu bỏ notification

Nhân viên vẫn có lý do tự nhiên để quay lại khi ticket mới được giao cần xử lý. Ticket mới là trigger bên ngoài của use case; notification chỉ giúp báo họ biết ticket đã đến, không tạo nhu cầu hỗ trợ và không phải value.

## Metric hypothesis

“**Nếu loop này hoạt động, metric NSM — số ticket duy nhất được giải quyết đạt tiêu chuẩn chất lượng trên mỗi nhân viên tuyến đầu — sẽ thay đổi theo hướng tăng trong các cohort ticket đến liên tiếp có cùng segment, sau khi từng ticket hoàn tất vòng đời và cửa sổ xác nhận 7 ngày, vì ticket mới tạo cơ hội phản hồi tự nhiên và chỉ những ticket thực sự được giải quyết có chất lượng mới được tính.**”

Hướng tăng có nghĩa là nhiều ticket hơn đạt chuẩn value, không chỉ nhiều bản nháp hoặc phản hồi được gửi; cần đọc cùng counter-metric reopen/liên hệ lại để kiểm tra chất lượng. Khung 7 ngày là giả định ở mục 03, không phải benchmark.

# 06 — Tracking nhanh

**Giả định triển khai:** event dưới đây là đề xuất, không khẳng định workspace đang có instrumentation. Event gửi/đổi trạng thái chỉ phát sau khi thay đổi thực sự được xác nhận và lưu. Tên metric giữ nguyên theo mục 03–04.

## Event plan

| Tên event | Ý nghĩa | Thời điểm ghi nhận | Metric sử dụng |
|---|---|---|---|
| `actionable_ticket_assigned` | **Input:** ticket đến cần phản hồi đã được giao cho nhân viên. | Khi assignment được lưu và ticket xuất hiện trong hàng xử lý của nhân viên; mỗi ticket–assignee chỉ ghi một lần cho lần giao này. | Activation — Start event; Retention — Cohort entry; Engagement Breadth — mẫu số ticket được giao. |
| `ai_draft_generated` | **AI output:** bản nháp đã được tạo đầy đủ và lưu/hiển thị cho ticket; không chứng minh nhân viên đã xem hoặc khách nhận value. | Khi output hoàn chỉnh được lưu cùng `ticket_id` và `draft_id`, không phải lúc bắt đầu gọi model. | Leading indicator: “Tỷ lệ ticket được giao có bản nháp AI được nhân viên đánh giá là liên quan và có căn cứ để rà soát” — xác định ticket có draft để đối chiếu; event này một mình không tính draft là usable. |
| `ai_draft_reviewed` | **Human review:** nhân viên hoàn tất rà soát và ghi kết quả liên quan/có căn cứ hoặc không; đây là đánh giá draft, chưa phải core action. | Khi review disposition được lưu cho `draft_id`; chỉ ghi một kết quả hoàn tất cho mỗi draft version. | Leading indicator: “Tỷ lệ ticket được giao có bản nháp AI được nhân viên đánh giá là liên quan và có căn cứ để rà soát” — tử số là ticket có kết quả review đạt; mẫu số là ticket đủ điều kiện được giao. |
| `support_response_sent` | **Core action:** phản hồi cuối cùng đã rà soát, trực tiếp trả lời yêu cầu và được gửi gắn với ticket. | Chỉ sau khi hệ thống xác nhận gửi thành công và lưu `response_id`; click gửi hoặc lỗi gửi không phát event. | Activation — Activation event; Engagement Breadth — tử số ticket có phản hồi gửi; Leading indicator — “Thời gian từ lúc giao ticket đến khi gửi phản hồi đã rà soát”. |
| `ticket_resolved` | **State change:** ticket thực sự chuyển sang trạng thái resolved. Đây là điều kiện của NSM, chưa đủ để khẳng định value. | Khi trạng thái resolved được lưu; ghi nhận transition thực tế từ trạng thái chưa resolved. | NSM — điều kiện resolved; Counter-metric — mẫu số ticket resolved đủ 7 ngày theo dõi. |
| `ticket_reopened` | **Counter:** ticket đã resolved thực sự chuyển lại sang trạng thái mở trong cửa sổ theo dõi. | Khi transition reopen được lưu; ghi một lần cho mỗi transition/ticket và giữ timestamp. | Counter-metric: “Tỷ lệ ticket bị mở lại hoặc khách liên hệ lại trong 7 ngày” — tử số đếm ticket duy nhất có ít nhất một lần reopen, không đếm số transition. |
| `customer_recontact_received` | **Counter:** khách thực sự gửi liên hệ tiếp theo được liên kết với ticket đã resolved; không suy diễn từ trạng thái hoặc nội dung AI. | Khi hệ thống nhận và liên kết một liên hệ mới trong 7 ngày sau resolve; cần khả năng nối liên hệ qua kênh liên quan. | Counter-metric: “Tỷ lệ ticket bị mở lại hoặc khách liên hệ lại trong 7 ngày” — tử số ticket có recontact; một ticket chỉ tính một lần dù có nhiều liên hệ, reopen hoặc cả hai. |
| `qualified_ticket_resolution` | **Derived value:** ticket đã resolved, QA xác nhận phản hồi liên quan/có căn cứ, và hết đủ 7 ngày không reopen hoặc recontact. Đây mới là event value; không đồng nhất với output AI hay `support_response_sent`. | Sau khi hết cửa sổ 7 ngày tính từ resolve, xác nhận đủ điều kiện QA và không có counter-event; ghi tối đa một lần cho mỗi `ticket_id`. | NSM — đếm ticket đạt chất lượng; Retention — Return event trên ticket tiếp theo. |

## Khoảng trống tracking cần xử lý

- Workspace chưa xác nhận có trường để nhân viên ghi nhận draft “liên quan và có căn cứ”, có quy trình QA, hoặc có nguồn dữ liệu liên kết recontact đa kênh. Nếu chưa có, cần bổ sung review disposition/QA và cơ chế nối ticket–liên hệ trước khi tính các leading indicator, NSM và counter-metric; không coi event draft/sent là proxy đã đủ.
- `qualified_ticket_resolution` là event tổng hợp cần được phát sau khi đủ điều kiện Phase 3; không phát ngay khi ticket chuyển resolved. Cửa sổ 7 ngày vẫn là giả định cần xác nhận.

## Thuộc tính event tối thiểu để tính metric

| Event | Thuộc tính/join cần có |
|---|---|
| `actionable_ticket_assigned` | `event_id`, `assigned_at`, `ticket_id`, `user_id` (nhân viên được giao), và `shift_end_at` hoặc lịch ca để tính activation window. Cần để nối cohort, đo breadth và retention cùng actor. |
| `ai_draft_generated` | `event_id`, `generated_at`, `ticket_id`, `draft_id`, `assigned_user_id` (để nối với nhân viên/cohort); dùng để nối output với ticket/review, không phải value. |
| `ai_draft_reviewed` | `event_id`, `reviewed_at`, `review_id`, `ticket_id`, `draft_id`, `user_id`, `review_disposition` (liên quan/có căn cứ hoặc không). Tử số leading indicator đếm ticket duy nhất có ít nhất một review đạt. |
| `support_response_sent` | `event_id`, `sent_at`, `ticket_id`, `response_id`, `review_id` (review đã hoàn tất), `draft_id` nếu dùng draft AI, `user_id`; cần nối cùng nhân viên với assignment, tính thời gian và đếm action một lần. |
| `ticket_resolved` | `event_id`, `resolved_at`, `ticket_id`, `transition_id`; mẫu số counter chỉ tính ticket duy nhất đủ 7 ngày theo dõi. |
| `ticket_reopened` | `event_id`, `occurred_at`, `ticket_id`, `transition_id`; metric đếm ticket duy nhất có ít nhất một lần reopen. |
| `customer_recontact_received` | `event_id`, `received_at`, `ticket_id`, `contact_id` và nguồn liên kết contact–ticket; metric đếm ticket duy nhất, không đếm nhiều contact thành nhiều ticket. |
| `qualified_ticket_resolution` | `event_id`, `confirmed_at`, `ticket_id`, `user_id` của nhân viên gửi phản hồi được tính, `resolved_at`, `qa_pass`; một event duy nhất cho mỗi ticket sau khi hết cửa sổ. |

Các ID và timestamp này là yêu cầu cho schema đề xuất, chưa được xác nhận là đang được sản phẩm ghi. Thiếu identity/linkage, lịch ca, disposition QA hoặc liên kết recontact thì metric tương ứng chưa tính được tin cậy; nếu không có lịch ca, cửa sổ activation “hết ca làm đầu tiên” chưa thể tính.

## Tiêu chí nghiệm thu

1. **Với mỗi `user_id`, `ticket_id` và `response_id`, khi nhân viên gửi phản hồi đã rà soát, chỉ ghi `support_response_sent` khi `review_id` đã hoàn tất và hệ thống xác nhận gửi thành công; lỗi gửi, click, reload hoặc retry cùng `response_id` không tạo event thành công trùng.**
2. **Với mỗi `ticket_id`, khi ticket chuyển sang resolved, chỉ ghi `ticket_resolved` cho transition đã lưu; reload/autosave không tạo transition hoặc event thứ hai. `qualified_ticket_resolution` chỉ được ghi một lần sau đủ 7 ngày nếu QA đạt và không có `ticket_reopened`/`customer_recontact_received`; nếu thiếu điều kiện thì không ghi.**
3. **Với mỗi `ticket_id` và `draft_id`, khi AI hoàn tất và lưu một draft version, ghi tối đa một `ai_draft_generated`; retry cùng generation id không tạo bản ghi trùng, còn generation lỗi/đang chạy thì không ghi event hoàn tất.**
4. **Với mỗi `transition_id`/`contact_id`, chỉ ghi `ticket_reopened` hoặc `customer_recontact_received` sau khi transition/liên hệ thực sự được lưu và liên kết ticket; retry cùng ID không tạo event trùng. Counter-metric đếm ticket duy nhất, dù có nhiều lần liên hệ/reopen.**

## Tự kiểm Gate 4

| Điều kiện | Kết quả | Căn cứ |
|---|---|---|
| Loop có ít nhất hai chu kỳ và lý do quay lại không cần notification | Đạt | Hai ticket đến độc lập tạo hai chu kỳ; nhu cầu xử lý ticket mới là trigger tự nhiên, notification chỉ báo tin. |
| Metric hypothesis trỏ tới metric Phase 3 | Đạt | Hypothesis nêu đúng NSM về ticket giải quyết đạt chuẩn trên mỗi nhân viên và dùng cửa sổ xác nhận Phase 3. |
| Mọi event map tới ít nhất một metric Phase 3 | Đạt | Cột Metric sử dụng map cả 8 event tới Activation, Breadth, NSM, Leading indicators, Counter-metric hoặc Retention. |
| Event chỉ ghi khi hành vi hoàn tất và có chống ghi trùng | Đạt | Thời điểm ghi nêu transition/điều kiện hoàn tất; tiêu chí nghiệm thu kiểm tra send success, đủ cửa sổ và idempotency. |

**Gate 4 đạt**, với điều kiện các khoảng trống instrumentation nêu trên được giải quyết trước khi xem số liệu là đầy đủ.

# Chặng 5 — Tự soi lỗi & nộp bài lab

## Checklist tự soi

1. **Đạt** — Core action là nhân viên rà soát/chỉnh sửa và gửi phản hồi cuối cùng có căn cứ cho ticket; không phải thao tác giao diện hay output AI. `support_response_sent` chỉ ghi sau khi gửi thành công.
2. **Đạt** — Activation bắt đầu từ ticket đủ điều kiện được giao và được xác nhận bằng core action đầu tiên; không dùng login/tour. Cửa sổ hết ca làm đầu tiên được ghi là giả định cần xác nhận; cần lịch ca hoặc `shift_end_at` để tính.
3. **Đạt** — Hành vi phát sinh theo từng ticket cần phản hồi; cadence, NSM và retention đều dùng ticket-cycle/opportunity, không ép lịch dashboard.
4. **Đạt** — Không cần notification để tạo nhu cầu quay lại: ticket mới được giao là trigger bên ngoài tự nhiên; notification chỉ báo tin.
5. **Đạt** — Retention dùng cơ hội ticket tiếp theo của cùng nhân viên, cùng segment, với cửa sổ theo lifecycle và 7 ngày xác nhận; nếu chưa có ticket tiếp theo thì chưa kết luận churn. Cửa sổ 7 ngày là giả định.
6. **Đạt** — Cả 8 event trong mục 06 map tới Activation, Engagement Breadth, NSM, Leading indicators, Counter-metric hoặc Retention ở mục 03–04.
7. **Đã sửa** — Đã bổ sung các identity/join key, timestamp, review disposition, QA và liên kết contact cần thiết để tính các metric từ event set; schema và nguồn dữ liệu là đề xuất, chưa xác nhận đang được tracking.

### Rationale cho lựa chọn giữ lại

**Retention theo cơ hội ticket, không theo ngày/tuần:** giữ custom window vì ticket đến là trigger tự nhiên duy nhất có căn cứ trong workspace; tác động là retention chỉ đọc được khi cùng nhân viên có ticket tiếp theo và ticket đó hoàn tất cửa sổ chất lượng, còn không có cơ hội thì để trạng thái chưa quan sát thay vì churn.

## Kết luận Gate 5

**Gate 5 đạt.** Đã đối chiếu đủ 7 câu và xử lý khoảng trống về thuộc tính nối event để metric có thể tính theo định nghĩa. Không đổi core action, cadence, retention definition, metric hay event set; các event, QA, recontact và ngưỡng/cửa sổ và lịch ca cần thiết vẫn được ghi rõ là đề xuất/nguồn dữ liệu cần xác nhận, không xem là instrumentation đã tồn tại.
