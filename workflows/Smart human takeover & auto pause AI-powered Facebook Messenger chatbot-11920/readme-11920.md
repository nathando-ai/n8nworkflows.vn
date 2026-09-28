---
title: "🤖 Tự động chuyển đổi người hỗ trợ khi chatbot AI Facebook Messenger bị tạm dừng"
description: "Hướng dẫn tự động hóa chuyển đổi người hỗ trợ khi chatbot AI Facebook Messenger bị tạm dừng bằng n8n. Giải pháp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-chuyen-doi-nguoi-ho-tro-khi-chatbot-ai-facebook-messenger-bi-tam-dung"
tags: [n8n, automation, no-code, chatbot, facebook]
keywords: [n8n workflow, tự động hóa, chatbot, facebook messenger, AI]
---

# 🤖 Tự động chuyển đổi người hỗ trợ khi chatbot AI Facebook Messenger bị tạm dừng

[Các sếp] có biết không? Khi chatbot AI Facebook Messenger bị tạm dừng, việc chuyển đổi sang người hỗ trợ thủ công lại tốn thời gian và dễ gây trễ phản hồi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động chuyển đổi**: Tự động chuyển đổi người hỗ trợ khi chatbot bị tạm dừng.
- **Tiết kiệm thời gian**: Giảm thời gian chờ đợi và phản hồi nhanh hơn.
- **Nâng cao trải nghiệm khách hàng**: Đảm bảo khách hàng luôn nhận được hỗ trợ kịp thời.
- **Tích hợp hoàn hảo**: Kết hợp với các công cụ khác như Google Sheets, Slack, Telegram...
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook Developer với quyền truy cập vào Facebook Messenger API.
- API Key của Google Gemini để sử dụng chatbot AI.
- Google Sheets để lưu trữ dữ liệu lịch sử chat.
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11920).
2. Nhấn nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Facebook Webhook**: Cấu hình webhook để nhận tin nhắn từ Facebook Messenger.
- **Google Gemini Chat Model**: Cấu hình API Key của Google Gemini để sử dụng chatbot AI.
- **Google Sheets**: Cấu hình Google Sheets để lưu trữ dữ liệu lịch sử chat.
- **DataTable**: Cấu hình các bảng dữ liệu để lưu trữ thông tin về các cuộc trò chuyện đã xử lý, chưa xử lý và đã tạm dừng.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Nhận thông báo khi có tin nhắn mới từ khách hàng.
- **Lưu log**: Lưu trữ log các cuộc trò chuyện để phân tích và cải thiện chất lượng hỗ trợ.
- **Gửi báo cáo định kỳ**: Gửi báo cáo định kỳ về số lượng tin nhắn đã xử lý, chưa xử lý và đã tạm dừng.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình chuyển đổi người hỗ trợ khi chatbot AI Facebook Messenger bị tạm dừng. Điều này giúp tiết kiệm thời gian, nâng cao trải nghiệm khách hàng và đảm bảo hoạt động liên tục 24/7. Hãy áp dụng ngay để tối ưu hóa quy trình hỗ trợ khách hàng của các sếp!