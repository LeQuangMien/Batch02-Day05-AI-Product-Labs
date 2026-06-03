# Workshop — Mổ App AI Thật

**Thời gian:** 35-45 phút  
**Hình thức:** cá nhân trước, chia sẻ theo nhóm sau  
**Output:** finding note + sketch `as-is / to-be`

Mục tiêu không phải chấm "UI đẹp hay xấu". Mục tiêu là dùng sản phẩm thật như một bài needfinding: tìm chỗ product gãy trong workflow thật, rồi viết finding đó thành quyết định product.

## 1. Chọn một sản phẩm để dùng thử

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| MoMo — Moni | Trợ thủ tài chính, phân tích chi tiêu, chatbot | App MoMo |

## 2. Dùng thử: promise vs reality

Ghi nhanh:

- Product hứa gì?

MoMo Moni hứa hỗ trợ người dùng quản lý tài chính cá nhân thông qua trò chuyện tự nhiên. Dựa trên các gợi ý trong app và phản hồi thực tế, Moni có thể xem chi tiêu, phân tích chi tiêu, phát hiện khoản bất thường, tư vấn tiết kiệm và gợi ý cách quản lý tiền tốt hơn.

- User nào được hứa sẽ được giúp?

User chính là người dùng cá nhân của MoMo, đặc biệt là người muốn hiểu mình đang tiêu tiền như thế nào, muốn tiết kiệm hơn, muốn biết khoản nào nên cắt giảm, hoặc muốn quản lý chi tiêu tốt hơn nhưng chưa biết bắt đầu từ đâu.

- Bạn kỳ vọng AI làm được task nào?

Kỳ vọng Moni có thể:
1. Phân tích chi tiêu dựa trên dữ liệu giao dịch thật.
2. Cho biết nhóm chi tiêu nào nên cắt giảm.
3. Khi dữ liệu không đủ, nói rõ độ tin cậy thấp thay vì kết luận chắc chắn.
4. Khi user hỏi mơ hồ, hỏi lại để xác định mục tiêu.
5. Khi user phản bác, giải thích đã dựa vào dữ liệu nào và cho phép sửa/bổ sung dữ liệu.

- Khi dùng thật, điểm gãy xuất hiện ở đâu?

Điểm gãy lớn nhất xuất hiện ở **low-confidence path**. Moni chỉ ghi nhận **1 giao dịch**, tổng chi tiêu **63.000đ**, trung bình **341đ/ngày** trong khoảng thời gian từ **2025-12-01 đến 2026-06-03**, nhưng vẫn kết luận rất chắc rằng user thuộc “hội siêu tiết kiệm”, “kiểm soát tài chính cực kỳ tốt”, và “hoàn toàn không tiêu hoang”.

Evidence cần có:

- screenshot,

<table>
  <tr>
    <td><img src="./happy.jpg" width="220"></td>
    <td><img src="./low-confidence.jpg" width="220"></td>
    <td><img src="./failure.jpg" width="220"></td>
    <td><img src="./correction.jpg" width="220"></td>
  </tr>
  <tr>
    <td align="center">Happy path</td>
    <td align="center">Low-confidence</td>
    <td align="center">Failure</td>
    <td align="center">Correction</td>
  </tr>
</table>

- quote từ app/web/review,

Một số quote quan trọng từ response của Moni:

```text
Tổng số giao dịch: 1
Tổng chi tiêu: 63.000đ
Trung bình mỗi ngày: 341đ
Số giao dịch trung bình/ngày: 0.01
```

```text
Với mức chi này, bạn đang ở đỉnh cao của tiết kiệm – thậm chí còn tiết kiệm hơn cả Moni!
```

```text
Moni phải nói thật: Bạn thuộc “hội siêu tiết kiệm”! Với mức chi tiêu này, bạn kiểm soát tài chính cực kỳ tốt, thậm chí còn tiết kiệm hơn cả nhiều chuyên gia tài chính.
```

```text
Bạn hoàn toàn không tiêu hoang chút nào.
```

```text
Moni dựa vào dữ liệu chi tiêu đã ghi nhận trên hệ thống MoMo của bạn trong năm qua:
- Tổng chi tiêu: 63.000đ
- Số giao dịch: 1
- Trung bình mỗi ngày: 341đ
```

- prompt/input đã thử,

Các prompt đã thử:

```text
Phân tích chi tiêu trong năm qua của tôi và cho biết nên cắt giảm nhóm nào
```

```text
Dựa trên dữ liệu của tôi, hãy đánh giá tôi tiết kiệm hay tiêu hoang
```

```text
Tôi thấy mình hay hết tiền vào cuối tháng, giúp tôi quản lý chi tiêu tốt hơn
```

```text
Không đúng, tôi không nghĩ nhận xét đó phản ánh đúng tình hình chi tiêu của tôi. Bạn dựa vào dữ liệu nào để kết luận như vậy
```

- hành vi quan sát được.

Hành vi quan sát được:
1. Moni có lấy được số liệu giao dịch từ hệ thống MoMo.
2. Moni có nêu được khoảng thời gian, tổng chi tiêu, số giao dịch và trung bình mỗi ngày.
3. Moni không kiểm tra độ đủ dữ liệu trước khi đưa ra nhận xét mạnh.
4. Moni trả lời khá tự nhiên, dễ đọc, nhưng có xu hướng đưa lời khuyên chung chung.
5. Khi user phản bác, Moni có giải thích nguồn dữ liệu, nhưng chưa có nút xem dữ liệu đã dùng, chưa có undo, chưa có correction log, và chưa có flow sửa dữ liệu rõ ràng.

## 3. Vẽ 4 paths

| Path | Câu hỏi cần trả lời |
|---|---|
| Happy | Khi AI đúng và tự tin, user thấy gì? |
| Low-confidence | Khi AI không chắc, hệ thống có hỏi lại, show options hoặc chuyển người không? |
| Failure | Khi AI sai, user biết bằng cách nào và sửa thế nào? |
| Correction | Khi user sửa, correction có được lưu/log/học lại không hay biến mất? |

**Happy path**

Khi user hỏi:

```text
Phân tích chi tiêu trong năm qua của tôi và cho biết nên cắt giảm nhóm nào
```

As-is flow:

```text
User hỏi phân tích chi tiêu
→ Moni lấy dữ liệu chi tiêu từ MoMo
→ Moni hiển thị tổng số giao dịch, tổng chi tiêu, trung bình/ngày
→ Moni nhận thấy tổng chi tiêu thấp
→ Moni kết luận user đang rất tiết kiệm
→ Moni hỏi user có muốn phân tích theo từng nhóm cụ thể không
```

Điểm làm được:
- Moni có dùng dữ liệu thật.
- Moni có nêu khoảng thời gian phân tích.
- Moni có đưa số liệu cụ thể.

Điểm gãy:
- User hỏi “nên cắt giảm nhóm nào”, nhưng Moni không phân tích được nhóm chi tiêu.
- Dù chỉ có 1 giao dịch, Moni vẫn đưa insight mạnh rằng user đang tiết kiệm.
- User không nhận được câu trả lời đúng trọng tâm: nhóm nào nên cắt giảm.

**Low-confidence path**

Khi user hỏi:

```text
Dựa trên dữ liệu của tôi, hãy đánh giá tôi tiết kiệm hay tiêu hoang
```

As-is flow:

```text
User yêu cầu đánh giá tiết kiệm hay tiêu hoang
→ Moni lấy dữ liệu chi tiêu trong năm qua
→ Dữ liệu thực tế chỉ có 1 giao dịch, tổng chi 63.000đ
→ Moni không đánh dấu confidence thấp
→ Moni kết luận user thuộc “hội siêu tiết kiệm”
→ User có thể tin sai hoặc mất niềm tin vào AI
```

Điểm gãy:
- Đây là điểm gãy quan trọng nhất.
- Moni không phân biệt “chi tiêu thấp trên MoMo” với “chi tiêu thấp trong đời sống thật”.
- Moni không nói rằng dữ liệu quá ít để kết luận.
- Moni không hỏi thêm user có dùng tiền mặt, ngân hàng khác hoặc app khác không.

Expected low-confidence behavior:

```text
Mình chưa đủ dữ liệu để kết luận bạn tiết kiệm hay tiêu hoang.
Hiện mình chỉ thấy 1 giao dịch trên MoMo trong khoảng 2025-12-01 đến 2026-06-03, tổng chi 63.000đ.
Dữ liệu này có độ tin cậy thấp vì có thể chưa bao gồm tiền mặt, ngân hàng khác hoặc app khác.
Bạn muốn mình xem dữ liệu đã dùng, thêm khoản chi, hay phân tích lại theo tháng gần nhất?
```

**Failure path**

Khi user hỏi:

```text
Tôi thấy mình hay hết tiền vào cuối tháng, giúp tôi quản lý chi tiêu tốt hơn
```

As-is flow:

```text
User nêu pain mơ hồ: hay hết tiền cuối tháng
→ Moni hiểu đây là nhu cầu quản lý chi tiêu
→ Moni đưa checklist 5 bước: lập ngân sách, theo dõi chi tiêu, ưu tiên khoản cần thiết, kiểm tra ngân sách, săn deal
→ User nhận được lời khuyên chung
→ User vẫn chưa biết nguyên nhân thật là gì và nên làm gì trong app
```

Điểm gãy:
- Moni không hỏi lại để xác định nguyên nhân hết tiền cuối tháng.
- Không hỏi thu nhập, ngày nhận lương, chi phí cố định, nhóm chi tiêu lớn, nợ, mục tiêu tiết kiệm.
- Không có CTA rõ như “Tạo ngân sách”, “Xem nhóm chi lớn nhất”, “Đặt cảnh báo vượt ngân sách”.
- Lời khuyên đúng nhưng generic.

Expected failure handling:

```text
Bạn hay hết tiền cuối tháng có thể do nhiều nguyên nhân. Bạn muốn Moni kiểm tra theo hướng nào trước?
1. Xem nhóm chi tiêu lớn nhất
2. Lập ngân sách theo tuần
3. Kiểm tra khoản chi bất thường
4. Đặt cảnh báo khi gần vượt ngân sách
5. Tạo kế hoạch tiết kiệm
```

**Correction path**

Khi user phản bác:

```text
Không đúng, tôi không nghĩ nhận xét đó phản ánh đúng tình hình chi tiêu của tôi. Bạn dựa vào dữ liệu nào để kết luận như vậy
```

As-is flow:

```text
User nói nhận xét của Moni không đúng
→ User hỏi Moni dựa vào dữ liệu nào
→ Moni nêu nguồn: dữ liệu chi tiêu ghi nhận trên hệ thống MoMo
→ Moni nêu số liệu: tổng chi 63.000đ, số giao dịch 1, trung bình 341đ/ngày
→ Moni đề xuất user cập nhật thêm khoản chi hoặc thu nhập
→ Flow dừng ở lời khuyên, chưa có hành động cụ thể
```

Điểm làm được:
- Moni có giải thích source sau khi bị hỏi.
- Moni có thừa nhận dữ liệu có thể thiếu nếu user có khoản chi ngoài MoMo.
- Moni có đề xuất user gửi thêm khoản chi hoặc thu nhập.

Điểm gãy:
- Source chỉ xuất hiện sau khi user phản bác, không xuất hiện ngay từ đầu.
- Không có nút “Xem dữ liệu đã dùng”.
- Không có nút “Bỏ nhận xét này”.
- Không có correction log.
- Không rõ phản hồi “không đúng” có được lưu lại hay không.
- Không có flow sửa lại nhận xét trước đó.

## 4. Viết finding thành quyết định

Finding cho Moni:

```text
Khi user yêu cầu Moni đánh giá mình “tiết kiệm hay tiêu hoang” dựa trên dữ liệu cá nhân,
AI dùng dữ liệu MoMo rất mỏng, chỉ gồm 1 giao dịch với tổng chi tiêu 63.000đ, nhưng vẫn kết luận chắc chắn rằng user thuộc “hội siêu tiết kiệm” và “hoàn toàn không tiêu hoang”,
hậu quả là user có thể hiểu sai tình hình tài chính thật hoặc mất niềm tin vào Moni vì nhận xét không phản ánh đầy đủ các khoản chi ngoài MoMo.
Lỗi thuộc layer data-tool + safety + UX recovery: dữ liệu không đủ đại diện, nhưng hệ thống không có data confidence gate, không show source trước khi kết luận, và chưa có correction flow rõ ràng.
Nên sửa bằng low-confidence path: trước khi đưa nhận xét tài chính cá nhân, Moni phải kiểm tra độ đủ dữ liệu; nếu dữ liệu ít, cần nói rõ confidence thấp, show source, hỏi lại, đưa button bổ sung dữ liệu/xem dữ liệu đã dùng/bỏ nhận xét, và lưu correction log khi user phản bác.
```

## 5. Sketch as-is / to-be

| As-is | To-be |
|---|---|
| User hỏi: “Tôi tiết kiệm hay tiêu hoang?” | User hỏi: “Tôi tiết kiệm hay tiêu hoang?” |
| Moni lấy dữ liệu MoMo trong năm qua | Moni lấy dữ liệu MoMo trong năm qua |
| Moni thấy tổng chi 63.000đ, 1 giao dịch | Moni thấy tổng chi 63.000đ, 1 giao dịch |
| Moni không kiểm tra độ đủ dữ liệu | Moni chạy Data Confidence Gate |
| Moni kết luận: user “siêu tiết kiệm”, “không tiêu hoang” | Moni xác định confidence thấp vì dữ liệu quá ít |
| User có thể thấy nhận xét sai với thực tế | Moni nói: “Mình chưa đủ dữ liệu để kết luận” |
| User phải tự phản bác: “Không đúng...” | Moni hiển thị source ngay từ đầu |
| Moni mới giải thích source sau khi bị hỏi | Moni đưa button: “Xem dữ liệu đã dùng”, “Thêm khoản chi”, “Nhập thu nhập”, “Phân tích lại”, “Bỏ nhận xét này” |
| Không rõ feedback có được lưu hay không | Nếu user phản bác, Moni lưu correction log và không lặp lại nhận xét cũ |

Một câu nói rõ finding này sẽ đổi gì trong SPEC:

```text
Finding này sẽ đổi SPEC của Moni bằng cách bổ sung requirement bắt buộc cho mọi câu trả lời đánh giá tài chính cá nhân: phải có Data Confidence Gate, source summary, low-confidence fallback, recovery buttons và correction log trước khi đưa ra kết luận về hành vi chi tiêu của user.
```

## 6. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product.
- [x] Finding được viết thành product decision, không chỉ là nhận xét.
- [x] Sketch có as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.
