---
title: "📧 Tự động gửi email theo dõi cá nhân hóa cho lịch hẹn Calendly với GPT-4 và Outlook"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình gửi email theo dõi cá nhân hóa sau khi khách hàng đặt lịch qua Calendly, sử dụng trí tuệ nhân tạo GPT-4 và tích hợp Outlook."
slug: "tu-dong-gui-email-theo-doi-ca-nhan-hoa-calendly-gpt4-outlook"
tags: [n8n, automation, no-code, Calendly, Outlook, GPT-4]
keywords: [n8n workflow, tự động hóa email, Calendly, Outlook, GPT-4]
---

# 📧 Tự động gửi email theo dõi cá nhân hóa cho lịch hẹn Calendly với GPT-4 và Outlook

[Các sếp đang gặp khó khăn khi phải gửi email theo dõi thủ công sau khi khách hàng đặt lịch qua Calendly. Quá trình này tốn thời gian, không cá nhân hóa và dễ bị lỗi. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này với trí tuệ nhân tạo GPT-4, đảm bảo email được cá nhân hóa và gửi ngay sau khi khách hàng đặt lịch.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi email theo dõi ngay sau khi khách hàng đặt lịch.
- **Cá nhân hóa cao**: Sử dụng GPT-4 để tạo nội dung email phù hợp với từng khách hàng.
- **Chính xác**: Dữ liệu lịch hẹn được lấy trực tiếp từ Calendly, đảm bảo thông tin chính xác.
- **Tích hợp Outlook**: Email được gửi qua Outlook, đảm bảo độ tin cậy và chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Calendly với quyền truy cập API.
- Tài khoản Outlook với quyền gửi email.
- API Key của OpenAI để sử dụng GPT-4.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/7306](https://n8n.io/workflows/7306).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node Calendly Event**:
  - Thêm credential Calendly API.
  - Đảm bảo node được cấu hình để lắng nghe sự kiện `invitee.created`.

- **Node Send a message2 (Microsoft Outlook)**:
  - Thêm credential Microsoft Outlook OAuth2.
  - Đảm bảo tài khoản Outlook có quyền gửi email.

- **Node OpenAI Chat Model1**:
  - Thêm credential OpenAI API.
  - Đảm bảo model được chọn là `gpt-4.1-mini`.

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để thông báo khi email được gửi thành công.
- **Lưu log**: Thêm node để lưu log các email đã gửi để theo dõi hiệu suất.
- **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp về số lượng email đã gửi trong một khoảng thời gian.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình gửi email theo dõi sau khi khách hàng đặt lịch qua Calendly, đảm bảo email được cá nhân hóa và gửi ngay lập tức. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao trải nghiệm khách hàng!