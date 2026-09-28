---
title: "🤖 WhatsApp Customer Support Bot với AI Gemini và Knowledge Base từ Google Docs"
description: "Tự động hóa hỗ trợ khách hàng trên WhatsApp với AI Gemini và cơ sở kiến thức từ Google Docs - Giải pháp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "whatsapp-customer-support-bot-gemini-google-docs"
tags: [n8n, automation, no-code, whatsapp, ai, google-docs, google-sheets]
keywords: [n8n workflow, tự động hóa, chatbot, whatsapp, ai, google docs, google sheets]
---

# 🤖 WhatsApp Customer Support Bot với AI Gemini và Knowledge Base từ Google Docs

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình hỗ trợ khách hàng qua WhatsApp
- Tích hợp AI Gemini để cung cấp câu trả lời thông minh và chính xác
- Sử dụng cơ sở kiến thức từ Google Docs để cập nhật thông tin mới nhất
- Lưu trữ lịch sử hội thoại trong Google Sheets cho phân tích sau này
- Giữ nhớ ngữ cảnh cuộc trò chuyện trong vòng 24 giờ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (hoặc Meta Business Suite)
- Tài khoản Google Cloud với API Gemini và Google Docs
- Google Sheet để lưu trữ lịch sử hội thoại
- Google Doc chứa cơ sở kiến thức của doanh nghiệp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6459)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "when message received" (whatsAppTrigger)**
   - Cấu hình credentials cho WhatsApp Trigger API
   - Đảm bảo webhook được thiết lập đúng trên Meta Business Suite

2. **Node "Google Gemini Chat Model" (lmChatGoogleGemini)**
   - Cấu hình credentials cho Google Palm API
   - Đặt temperature và topP theo nhu cầu (thường 0.7-0.9 cho câu trả lời cân bằng)

3. **Node "company's knowledge" (googleDocs)**
   - Cấu hình credentials cho Google Docs OAuth2 API
   - Nhập ID của Google Doc chứa cơ sở kiến thức
   - Chọn đúng phạm vi dữ liệu cần lấy (thường là toàn bộ nội dung)

4. **Node "Append or update row in sheet" (googleSheets)**
   - Cấu hình credentials cho Google Sheets OAuth2 API
   - Nhập ID của Google Sheet để lưu lịch sử
   - Đặt tên sheet và cấu hình các cột cần ghi dữ liệu

5. **Node "Simple Memory" (memoryBufferWindow)**
   - Đặt kWindow (kích thước cửa sổ nhớ) phù hợp (thường 5-10)

#### 3. Kích hoạt ⚡️
- Test run với một số câu hỏi mẫu để kiểm tra toàn bộ chuỗi xử lý
- Kiểm tra lịch sử lưu trong Google Sheet
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có câu hỏi mới
- Thêm node để gửi báo cáo hàng ngày về các câu hỏi thường gặp
- Tích hợp với hệ thống CRM để theo dõi khách hàng
- Sử dụng AI để phân loại câu hỏi và tự động chuyển tiếp đến nhân viên phù hợp

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa hỗ trợ khách hàng qua WhatsApp với AI Gemini và cơ sở kiến thức từ Google Docs. Với việc tích hợp hoàn chỉnh với Google Sheets, các sếp có thể dễ dàng quản lý và phân tích dữ liệu hội thoại. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tiết kiệm thời gian cho đội ngũ hỗ trợ!