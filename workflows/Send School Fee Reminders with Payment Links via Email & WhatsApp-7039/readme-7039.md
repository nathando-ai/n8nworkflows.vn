---
title: "💰 Tự động nhắc nhở học phí qua Email & WhatsApp - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn tự động hóa nhắc nhở học phí cho trường học qua email và WhatsApp bằng n8n. Tiết kiệm thời gian, tăng hiệu quả nhắc nhở và giảm công việc thủ công."
slug: "tu-dong-nhac-nho-hoc-phi-email-whatsapp-n8n"
tags: [n8n, automation, no-code, education, school-management]
keywords: [n8n workflow, tự động hóa học phí, nhắc nhở học phí, email học phí, WhatsApp học phí]
---

# 💰 Tự động nhắc nhở học phí qua Email & WhatsApp - Workflow n8n hoàn chỉnh

[Các sếp trường học và quản lý học phí đang gặp khó khăn khi phải nhắc nhở học phí cho hàng trăm học sinh mỗi ngày. Việc này tốn thời gian, dễ bỏ sót và không cá nhân hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình nhắc nhở học phí qua email và WhatsApp, tiết kiệm thời gian và tăng hiệu quả nhắc nhở.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động nhắc nhở học phí hàng ngày mà không cần can thiệp thủ công.
- **Tăng hiệu quả nhắc nhở**: Đảm bảo học sinh nhận được thông báo kịp thời.
- **Cá nhân hóa**: Tùy chỉnh nội dung nhắc nhở cho từng học sinh.
- **Giảm công việc thủ công**: Hệ thống tự động xử lý toàn bộ quy trình từ đọc dữ liệu đến gửi thông báo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft Excel chứa danh sách học phí (cần chia sẻ với n8n).
- Tài khoản email để gửi thông báo (SMTP credentials).
- Tài khoản WhatsApp Business API để gửi tin nhắn.
- Dữ liệu học phí phải có các trường: Student Name, Phone Number, Fee Amount, Due Date, Payment Link.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7039](https://n8n.io/workflows/7039)
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Daily Fee Check - 8 AM"**: Đảm bảo thời gian chạy phù hợp với lịch làm việc của các sếp.
- **Node "Read Pending Fees"**:
  - Chọn credentials "microsoftExcelOAuth2Api".
  - Điền thông tin Sheet ID và Sheet Name chứa dữ liệu học phí.
- **Node "Process Fee Reminders"**:
  - Kiểm tra và chỉnh sửa code để lọc học phí đến hạn trong 3 ngày.
  - Đảm bảo code tạo đúng URL thanh toán.
- **Node "Prepare Email Reminder"**:
  - Chỉnh sửa template email để phù hợp với thương hiệu trường học.
  - Đảm bảo biến {{paymentLink}} được giữ nguyên.
- **Node "Prepare WhatsApp Reminder"**:
  - Chỉnh sửa template tin nhắn WhatsApp để phù hợp với thương hiệu trường học.
  - Đảm bảo biến {{paymentLink}} được giữ nguyên.
- **Node "Send Email Reminder"**:
  - Chọn credentials "smtp".
  - Điền thông tin email gửi và chủ đề email.
- **Node "Update Reminder Status"**:
  - Chọn credentials "microsoftExcelOAuth2Api".
  - Điền thông tin Sheet ID và Sheet Name để cập nhật trạng thái nhắc nhở.
- **Node "Send message"**:
  - Chọn credentials "whatsAppApi".
  - Đảm bảo số điện thoại học sinh được truyền đúng vào node này.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" để kích hoạt workflow.
2. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
3. Sau khi test thành công, workflow sẽ tự động chạy hàng ngày lúc 8 AM.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node gửi thông báo lên Slack khi có lỗi xảy ra.
- **Lưu log nhắc nhở**: Thêm node ghi log các nhắc nhở đã gửi để theo dõi.
- **Gửi báo cáo hàng tuần**: Thêm node tổng hợp báo cáo nhắc nhở hàng tuần và gửi qua email.
- **Tích hợp với hệ thống thanh toán**: Kết nối với cổng thanh toán trực tuyến để tự động cập nhật trạng thái thanh toán.

### 📌 Kết luận
Workflow này giúp các sếp trường học tự động hóa toàn bộ quy trình nhắc nhở học phí, tiết kiệm thời gian và tăng hiệu quả nhắc nhở. Các sếp chỉ cần chuẩn bị dữ liệu và cấu hình các credentials cần thiết, sau đó workflow sẽ tự động chạy hàng ngày và gửi nhắc nhở qua email và WhatsApp cho học sinh. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý học phí của trường học!