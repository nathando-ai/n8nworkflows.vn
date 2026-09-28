---
title: "💰 Theo dõi chi tiêu đơn giản với n8n, AI và Google Sheets"
description: "Hướng dẫn tự động hóa việc ghi chép chi tiêu qua tin nhắn chat, chuyển đổi dữ liệu thành JSON và lưu vào Google Sheets một cách hoàn toàn không cần code."
slug: "theo-doi-chi-tieu-voi-n8n-ai-google-sheets"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, theo dõi chi tiêu, google sheets, openai]
---

# 💰 Theo dõi chi tiêu đơn giản với n8n, AI và Google Sheets

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải ghi chép chi tiêu hàng ngày vào bảng tính thủ công? Với workflow này, các sếp có thể dễ dàng ghi lại mọi khoản chi tiêu chỉ bằng cách nhắn tin qua chat, và hệ thống sẽ tự động chuyển đổi thông tin thành dữ liệu có cấu trúc và lưu vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Ghi chép chi tiêu chỉ trong vài giây qua tin nhắn chat.
- **Dữ liệu chính xác**: AI tự động chuyển đổi tin nhắn thành dữ liệu có cấu trúc.
- **Tích hợp dễ dàng**: Dữ liệu được lưu tự động vào Google Sheets, dễ dàng truy cập và phân tích.
- **Hoạt động liên tục**: Workflow hoạt động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng AI chat model).
- Tài khoản Google Sheets (để lưu dữ liệu chi tiêu).
- Tài khoản n8n (để triển khai workflow).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: `https://n8n.io/workflows/2819`.
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/2819) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets**:
   - Clone Google Sheet mẫu từ [đây](https://docs.google.com/spreadsheets/d/1D0r3tun7LF7Ypb21CmbTKEtn76WE-kaHvBCM5NdgiPU/edit?gid=0#gid=0).
   - Chọn sheet đã clone vào node "Save expense into Google Sheets".
   - Đảm bảo đã cấu hình Google Sheets OAuth2 trong n8n.

2. **OpenAI API**:
   - Tạo credentials cho OpenAI API trong n8n.
   - Cấu hình API key trong node "OpenAI Chat Model" và "OpenAI Chat Model1".

3. **Sub-workflow**:
   - Mở node "Parse msg and save to Sheets".
   - Chọn workflow hiện tại trong dropdown để đảm bảo sub-workflow hoạt động đúng.

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Activate" để kích hoạt workflow.
2. Test với tin nhắn mẫu: "car wash; 59.3 usd; 25 jan 2024".
3. Kiểm tra kết quả trong Google Sheets và tin nhắn phản hồi từ AI.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thay đổi node "When chat message received" để tích hợp với Slack hoặc Telegram.
- **Lưu log**: Thêm node để lưu log các tin nhắn và phản hồi từ AI.
- **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo chi tiêu hàng tuần qua email.
- **Tích hợp với các dịch vụ tài chính**: Kết nối với các dịch vụ ngân hàng để tự động đồng bộ dữ liệu chi tiêu.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi khi ghi chép chi tiêu hàng ngày. Với sự kết hợp của AI và Google Sheets, dữ liệu được quản lý một cách hiệu quả và dễ dàng truy cập. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!