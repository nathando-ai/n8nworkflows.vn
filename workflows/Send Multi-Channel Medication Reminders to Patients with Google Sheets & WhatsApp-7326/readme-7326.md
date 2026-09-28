---
title: "💊 Tự động nhắc nhở uống thuốc đa kênh với Google Sheets & WhatsApp"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp các bệnh viện, phòng khám gửi nhắc nhở uống thuốc qua WhatsApp và email, tăng tính cá nhân hóa và hiệu quả nhắc nhở."
slug: "tu-dong-nhac-nho-uong-thuoc-da-kenh"
tags: [n8n, automation, no-code, google-sheets, whatsapp, healthcare]
keywords: [n8n workflow, tự động hóa nhắc nhở uống thuốc, google sheets, whatsApp, tự động hóa y tế]
---

# 💊 Tự động nhắc nhở uống thuốc đa kênh với Google Sheets & WhatsApp

[Các sếp y tế] thường gặp khó khăn khi phải nhắc nhở bệnh nhân uống thuốc theo lịch trình. Việc này thường phải thực hiện thủ công, dễ gây lỗi và không hiệu quả. Workflow này giúp tự động hóa toàn bộ quy trình từ tạo lịch nhắc nhở đến gửi thông báo qua WhatsApp và email, đảm bảo bệnh nhân nhận được nhắc nhở đúng giờ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình nhắc nhở.
- **Chính xác cao**: Không bỏ sót lịch nhắc nhở nào.
- **Cá nhân hóa**: Gửi thông báo theo lịch trình cá nhân của từng bệnh nhân.
- **Hoạt động liên tục**: Nhắc nhở được gửi đúng giờ 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt.
- Tài khoản WhatsApp Business API.
- Tài khoản email SMTP để gửi thông báo.
- Dữ liệu bệnh nhân trong Google Sheets với các cột: `patient_id`, `phone_number`, `email`, `medication`, `schedule`, `status`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/7326).
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Watch Sheet For Trigger"**:
   - Chọn credentials là `googleSheetsTriggerOAuth2Api`.
   - Điền `Spreadsheet ID` và `Sheet Name` chứa dữ liệu bệnh nhân.

2. **Node "Save Reminders" và "Mark as Processed"**:
   - Chọn credentials là `googleApi`.
   - Điền `Spreadsheet ID` và `Sheet Name` để lưu lịch nhắc nhở.
   - Đảm bảo các cột `patient_id`, `phone_number`, `email`, `medication`, `schedule`, `status` đã được tạo trong sheet.

3. **Node "Send WhatsApp"**:
   - Chọn credentials là `whatsAppApi`.
   - Điền `Phone Number ID` và `Template Name` cho tin nhắn WhatsApp.

4. **Node "Send email"**:
   - Chọn credentials là `smtp`.
   - Điền `From`, `To`, `Subject` và `Body` cho email nhắc nhở.

5. **Node "Create Reminder Schedule" và "Find Due Reminders"**:
   - Chỉnh sửa mã JavaScript trong các node này để phù hợp với định dạng dữ liệu của các sếp.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu gửi nhắc nhở tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo qua Slack hoặc Telegram cho đội ngũ y tế.
- **Lưu log**: Thêm node để lưu log các tin nhắn đã gửi để theo dõi hiệu quả nhắc nhở.
- **Gửi báo cáo định kỳ**: Tạo báo cáo tổng hợp các nhắc nhở đã gửi và tỷ lệ phản hồi.

### 📌 Kết luận
Workflow này giúp các sếp y tế tự động hóa toàn bộ quy trình nhắc nhở uống thuốc, tăng tính cá nhân hóa và hiệu quả nhắc nhở. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao chất lượng dịch vụ chăm sóc sức khỏe!