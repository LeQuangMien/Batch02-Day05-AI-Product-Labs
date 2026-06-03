# Template — Evidence Pack

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:**  
**Track:**  
**Product/app đã chọn:**  
**Build slice đang nghĩ:**  

## 2. Self-use evidence

Nhóm tự dùng app/workflow và ghi lại điểm gãy.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Người dùng tương tác theo kịch bản đề xuất của AI để thiết lập mục tiêu, nhưng tính năng cốt lõi bị lỗi hệ thống khiến flow bị đứt gãy. | <img src="anh3.jpg" width="150"/> | Failure | Tính năng thông báo lỗi hệ thống trực tiếp làm giảm độ tin cậy của trợ lý AI. Cần có cơ chế ghi nhận tạm thời thay vì từ chối user. |
| AI yêu cầu người dùng nhập tay hoàn toàn, không có cơ chế đồng bộ tự động hoặc quét hóa đơn/bill chuyển khoản. | <img src="anh2.jpg" width="150"/> | Low-confidence / Failure | Người dùng rất dễ bỏ cuộc nếu phải tự gõ từng khoản chi tiêu. Cần tối ưu hóa bằng cách cho phép chụp ảnh hóa đơn/gửi ảnh chụp màn hình chuyển khoản ngân hàng. |

## 3. User / review / social evidence

Nguồn có thể là review App Store/Play, group, comment, phỏng vấn nhanh, hoặc nguồn public khác.

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| "App thông minh nhưng mỗi lần chi tiêu lại phải vào nhắn tin mệt quá, nhiều khi quên không nhập là cuối tháng lệch hết số liệu." | Giả định từ hành vi ở Ảnh 2 | Người đi làm bận rộn, muốn quản lý tài chính tinh gọn. | Ngại nhập tay, lười tương tác liên tục dẫn đến việc bỏ quên không cập nhật dữ liệu (Data fragmentation). |
| "Đang định lên kế hoạch tiết kiệm tiền mua máy ảnh theo gợi ý của bot thì báo lỗi hệ thống, bắt tự ghi tay ra chỗ khác thì dùng AI làm gì nữa." | Giả định từ tình huống ở Ảnh 3 | Sinh viên/Người trẻ có mục tiêu tài chính ngắn hạn. | Lỗi tính năng cốt lõi (Core feature broken), AI phản hồi bất lực buộc người dùng phải dùng phương pháp thủ công bên ngoài. |

```text
Đây là giả định. Nhóm sẽ kiểm bằng [cách phỏng vấn nhanh 3 người dùng thử kịch bản này và đọc review trên store] trước checkpoint M1 Day 06.
```
| Ảnh 2 | Ảnh 3 |
|---|---|
| <img src="anh2.jpg" width="150" />| <img src="anh3.jpg" width="150"/> |
## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| **Finizi / Money Lover** (Tính năng lập ngân sách) | Cho phép người dùng chọn nhanh các hạn mức ngân sách định sẵn hoặc gợi ý ngân sách dựa trên lịch sử chi tiêu tháng trước, thay vì bắt nhập tay từ số không. | **Pattern: Smart Defaults & Suggestions** (Gợi ý thông minh dựa trên ngữ cảnh). Giảm tải nhận thức cho user khi thiết lập mục tiêu tài chính. | **Có.** Thiết lập sẵn 3 mức ngân sách tiết kiệm cố định (ví dụ: 10%, 20%, 30% thu nhập) để user bấm chọn nhanh trong khung chat. |
| **Copilot Money / Cleo** (AI Financial Bot) | Khi hệ thống gặp lỗi kết nối hoặc không xử lý được request, bot sẽ chuyển hướng sang chế độ "Friendly Fallback" - xin lỗi một cách dí dỏm và chủ động mở một Form ngắn (Mini-App/Webview) để user điền nhanh thông tin, cam kết sẽ đồng bộ lại ngay khi hệ thống ổn định. | **Pattern: Graceful Degradation & Alternative Path** (Sụp đổ mượt mà và mở đường lui). Tuyệt đối không đẩy việc thủ công (ghi chép ngoài) hoàn toàn cho user. | **Có.** Code một câu thoại Fallback mới cho bot kèm theo một link Google Form hoặc Form Mini tích hợp sẵn để lưu nhanh mục tiêu tiết kiệm của user khi API lỗi. |

## 5. Evidence -> Insight

```text
Evidence nổi bật nhất:
Moni thông báo lỗi hệ thống ngay khi người dùng đồng ý thiết lập ngân sách tiết kiệm (Ảnh 3) và yêu cầu người dùng tự ghi chú thủ công ra bên ngoài trong khi hệ thống không hỗ trợ đồng bộ tự động (Ảnh 2).

Insight:
User không chỉ gặp lỗi kỹ thuật gián đoạn tính năng (Surface problem).
Thật ra họ cần sự an tâm và một giải pháp thay thế liền mạch ngay tại thời điểm đó (Trust & Recovery). Khi AI "bất lực" và đẩy toàn bộ việc theo dõi thủ công sang cho user, niềm tin vào một "Trợ lý tài chính thông minh" bị đổ vỡ hoàn toàn, khiến họ có xu hướng rời bỏ app vì ma sát nhập liệu quá lớn.

Opportunity:
AI có thể giúp bằng cách tự động tạo một lệnh "Ghi nhớ mục tiêu" tạm thời bằng ngôn ngữ tự nhiên (Augment hành động hẹp) kể cả khi tính năng ngân sách chính đang lỗi, hoặc chủ động nhắc nhở user định kỳ để bù đắp cho việc thiếu đồng bộ ngân hàng tự động.
```
| Ảnh 2 | Ảnh 3 |
|---|---|
| <img src="anh2.jpg" width="150" />| <img src="anh3.jpg" width="150"/> |

## 6. Evidence đổi SPEC như thế nào?

- [ ] Đổi user chính.
- [ ] Đổi pain statement.
- [x] Đổi build slice.
- [ ] Đổi Auto/Aug decision.
- [x] Đổi 4 paths.
- [x] Đổi failure mode.
- [ ] Đổi owner/test plan.

Ghi rõ 1-2 thay đổi quan trọng:

```text
Trước evidence, nhóm định:
Tập trung build flow "Happy Path" thật mượt mà từ lúc chat đến lúc tạo thành công ngân sách tiết kiệm, bỏ qua việc thiết kế kịch bản xử lý lỗi sâu (Failure path) và mặc định user sẽ kiên nhẫn gõ tay lại dữ liệu.

Sau evidence, nhóm đổi thành:
1. Thu hẹp Build Slice: Ưu tiên làm phần "Kịch bản dự phòng khi lỗi hệ thống (Fallback Recovery Flow)" lên mức ưu tiên cao nhất, xây dựng tính năng ghi nhận dữ liệu tạm thời (Temporary Data Catching) bằng Chat.
2. Thiết kế lại Failure Path: Định nghĩa lại cách xử lý khi tính năng lỗi - không để AI nói "không làm được", mà AI sẽ chủ động đề xuất giải pháp thay thế (ví dụ: "Moni chưa lưu vào ví lớn được, nhưng Moni đã ghi sổ tay tạm thời cho bạn rồi nhé!").

Lý do:
Trải nghiệm thực tế cho thấy điểm gãy ở Failure Path gây ức chế rất lớn cho user. Hệ thống chưa tự động đồng bộ (Ảnh 2) đã là một điểm trừ lớn về mặt thao tác, nếu gặp thêm lỗi hệ thống (Ảnh 3) mà không có phương án bọc lót (Recovery) tốt thì 100% user sẽ bỏ cuộc ngay lập tức.
```