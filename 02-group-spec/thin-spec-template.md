# Template — Thin SPEC Cuối Day 05

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.

## 1. Track, product/app và user

**Track:** AI Assistant / FinTech  
**Product/app thật:** Trợ thủ AI - Moni (Trợ lý quản lý tài chính cá nhân qua Chatbot).  
**User cụ thể:** Người trẻ (sinh viên, người mới đi làm) có nhu cầu tiết kiệm tiền cho các mục tiêu ngắn hạn nhưng bận rộn, ngại nhập liệu thủ công và dễ nản lòng khi gặp lỗi hệ thống.  
**Nhóm có phải user thật không? Nếu không, khác ở đâu?** Có. Nhóm chính là những người trẻ đang tự trải nghiệm, trực tiếp dùng app để lên kế hoạch tiết kiệm và tự vấp phải điểm gãy của hệ thống (System Failure).

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Lỗi hệ thống khi thiết lập ngân sách tiết kiệm (Ảnh 3). | Tự trải nghiệm sản phẩm (Self-use) | User bị cắt đứt kịch bản sử dụng (flow) ngay tại tính năng cốt lõi. AI đẩy phần việc thủ công bắt user tự ghi nhớ ra ngoài khiến trải nghiệm tệ đi. | Ưu tiên tối cao việc thiết kế **Failure Path** và **Fallback Recovery Flow** (AI ghi nhận dữ liệu tạm thời thay vì từ chối). |
| AI không tự động đồng bộ tài khoản, bắt nhập tay hoàn toàn (Ảnh 2). | Tự trải nghiệm sản phẩm (Self-use) | Ma sát nhập liệu (Input friction) rất lớn. Nếu kết hợp thêm lỗi hệ thống, user sẽ bỏ app ngay lập tức. | Giảm tải việc nhập liệu bằng cách thiết kế các nút chọn nhanh (**Smart Defaults**) trong kịch bản chat. |

| Ảnh 2 | Ảnh 3 |
|---|---|
| <img src="anh2.jpg" width="150" />| <img src="anh3.jpg" width="150"/> |

## 3. Pain statement

```text
User [người trẻ muốn tích lũy ngắn hạn] đang gặp khó ở [bước thiết lập kế hoạch và ngân sách tiết kiệm],
vì [hệ thống bất ngờ báo lỗi kỹ thuật và không có cơ chế tự động đồng bộ/sao lưu dữ liệu tạm thời, bắt người dùng phải tự ghi chép thủ công bên ngoài],
dẫn tới [user cảm thấy hụt hẫng, mất niềm tin vào sự "thông minh" của trợ lý AI và từ bỏ việc theo dõi tài chính vì quá phiền phức].
Bằng chứng chính là [ảnh chụp màn hình Moni báo lỗi hệ thống ở ảnh 3 và thông báo bắt nhập liệu thủ công hoàn toàn ở ảnh 2].
```

## 4. Build slice

```text
Cho [người trẻ đang muốn lên kế hoạch tiết kiệm 5 triệu trong 3 tháng],
prototype sẽ dùng AI để [Augment hành động ghi nhận và phân bổ dòng tiền bằng cách tự động tạo lệnh ghi nhớ tạm thời qua hội thoại (kể cả khi tính năng gốc bị lỗi)],
tạo ra [Kế hoạch phân bổ tiết kiệm hàng tháng rõ ràng dưới dạng tin nhắn tóm tắt kèm nút xác nhận nhanh],
và xử lý [failure mode (lỗi API/hệ thống)] bằng [mitigation: Chuyển hướng mượt mà sang chế độ ghi sổ tạm thời "Moni Note" và nhắc nhở user điền vào Mini-Form khi hệ thống ổn định trở lại].
```

## 5. Auto/Aug decision

Chọn một:

- [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Tài chính là vấn đề nhạy cảm và ứng dụng chưa đồng bộ tài khoản ngân hàng thật (Ảnh 2). Do đó, AI chỉ nên đóng vai trò trợ lý tính toán, đưa ra các gợi ý chia nhỏ dòng tiền và tạo kịch bản nhắc nhở, quyền quyết định lưu hoặc kích hoạt kế hoạch cuối cùng phải thuộc về user để đảm bảo tính chính xác và bảo mật.  
**Human role:** decider / reviewer  

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| **Happy** | User nhập mục tiêu "Tiết kiệm 5tr/3 tháng". AI tính toán ra con số ~1.666.667đ/tháng, gợi ý các mốc nạp tiền và tạo ngay một ví tiết kiệm ảo thành công ngay trong chat kèm lời động viên. |
| **Low-confidence** | User nhập câu mơ hồ "Muốn tiết kiệm tiền mua điện thoại". AI không biết số tiền và thời gian -> AI chủ động hỏi lại bằng menu lựa chọn gợi ý (Ví dụ: 5 triệu, 10 triệu hay 20 triệu?) thay vì bắt user tự nghĩ. |
| **Failure** | Hệ thống cốt lõi bị lỗi kết nối dữ liệu (như Ảnh 3). AI không báo lỗi kỹ thuật khô khan mà chủ động xin lỗi khéo léo và kích hoạt kịch bản dự phòng: "Moni đang bảo trì ví lớn, nhưng đã mở sẵn Sổ tay tạm thời để ghi nhận mục tiêu 5 triệu của bạn rồi nhé!". |
| **Correction** | User bấm nhầm mục tiêu hoặc muốn đổi từ 3 tháng thành 5 tháng. Prototype hiển thị ngay nút "Sửa mục tiêu" trực quan dưới bong bóng chat để cập nhật lại phép toán chia tiền mà không cần nhập lại từ đầu. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu user [gặp lỗi hệ thống liên tục khi đang hào hứng thiết lập mục tiêu tiết kiệm đầu tiên],
AI có thể [phản hồi bất lực, báo lỗi hệ thống khô khan và yêu cầu user tự ghi chép thủ công ra bên ngoài],
hậu quả là [user cảm thấy app vô dụng, nghi ngờ năng lực kỹ thuật của hệ thống và lập tức gỡ ứng dụng (Churn)].
Prototype sẽ xử lý bằng [fallback: tự động chuyển sang luồng "Ghi nhận tạm thời" bằng ngôn ngữ tự nhiên và cung cấp một Mini-Form điền nhanh để đồng bộ sau].
Owner kiểm thử path này là: [Tên thành viên phụ trách Tech/UX của nhóm].
```

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| Trần Đức Tâm - 2A202600803 | Research / evidence |  |
| KimHongGiang - 2A202600600 | SPEC |  |
| TranNgocThuy - 2A202600799 | Prototype |  |
| Lê Quốc Bảo - 2A202600561 | Test / failure path |  |
| LeQuangMien - 2A202600715 | Demo script / repo |  |
