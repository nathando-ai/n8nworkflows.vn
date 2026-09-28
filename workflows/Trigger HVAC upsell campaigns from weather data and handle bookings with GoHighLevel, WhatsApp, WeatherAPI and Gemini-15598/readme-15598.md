---
title: "🌡️ [Tự động hóa HVAC] Workflow n8n kích hoạt chiến dịch bán hàng dựa trên dữ liệu thời tiết và xử lý đặt lịch qua WhatsApp"
description: "Workflow n8n tự động hóa 100% không cần code giúp doanh nghiệp HVAC phát hiện nguy cơ thời tiết (nhiệt độ cao, lũ tuyết) và kích hoạt chiến dịch bán hàng thông qua WhatsApp, đồng thời xử lý đặt lịch qua AI chatbot Gemini."
slug: "tu-dong-hoa-hvac-weather-upsell-whatsApp"
tags: [n8n, automation, no-code, HVAC, CRM, WhatsApp, AI]
keywords: [n8n workflow, tự động hóa HVAC, bán hàng dựa trên thời tiết, chatbot WhatsApp, GoHighLevel, Gemini AI]
---

# 🌡️ Tự động hóa chiến dịch bán hàng HVAC dựa trên dữ liệu thời tiết và xử lý đặt lịch qua WhatsApp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp HVAC khi phải theo dõi thủ công dữ liệu thời tiết và quản lý khách hàng tiềm năng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phát hiện nguy cơ thời tiết (nhiệt độ cao, lũ tuyết) thông qua dữ liệu thời tiết.
- Tạo cơ hội bán hàng tự động cho khách hàng tiềm năng dựa trên dữ liệu thời tiết.
- Xử lý đặt lịch qua WhatsApp thông qua AI chatbot Gemini.
- Tiết kiệm thời gian và nhân lực cho đội ngũ kinh doanh.
- Tăng tỷ lệ chuyển đổi khách hàng tiềm năng thành khách hàng thực.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GoHighLevel (CRM) và API key.
- Tài khoản WhatsApp Business API và số điện thoại được ủy quyền.
- API key từ WeatherAPI.
- API key từ Google Gemini.
- Redis server cho lưu trữ lịch sử chat.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Fetch Contacts** (highLevel): Cấu hình credentials `highLevelOAuth2Api` và chọn operation `getAll`.
- **Update Contact City** (highLevel): Cấu hình credentials `highLevelOAuth2Api` và chọn operation `update`.
- **Fetch Weather Forecast** (httpRequest): Cấu hình credentials `httpQueryAuth` và nhập URL API WeatherAPI.
- **Send WhatsApp Template** (whatsApp): Cấu hình credentials `whatsAppApi` và chọn operation `send`.
- **Gemini Chat Model** (lmChatGoogleGemini): Cấu hình credentials `googlePalmApi` và nhập API key từ Google Gemini.
- **Redis Chat History Memory** (memoryRedisChat): Cấu hình credentials `redis` và nhập thông tin kết nối Redis server.
- **When WhatsApp Message Received** (whatsAppTrigger): Cấu hình credentials `whatsAppTriggerApi` và nhập thông tin số điện thoại được ủy quyền.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có khách hàng tiềm năng mới.
- Lưu log các hoạt động để theo dõi hiệu quả chiến dịch.
- Gửi báo cáo định kỳ về hiệu quả chiến dịch bán hàng dựa trên dữ liệu thời tiết.

### 📌 Kết luận
Workflow này giúp các doanh nghiệp HVAC tự động hóa quy trình bán hàng dựa trên dữ liệu thời tiết, tăng tỷ lệ chuyển đổi khách hàng tiềm năng và tiết kiệm thời gian cho đội ngũ kinh doanh. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của bạn!