---
title: "🌍 [AI Travel Planner] Tự động hóa kế hoạch du lịch với Telegram và OpenAI"
description: "Hướng dẫn tự động hóa kế hoạch du lịch thông minh bằng n8n, Telegram và OpenAI. Tiết kiệm thời gian lên đến 80% cho các chuyến đi công tác."
slug: "ai-travel-planner-telegram-openai"
tags: [n8n, automation, no-code, ai, telegram, openai]
keywords: [n8n workflow, tự động hóa du lịch, ai travel planner, telegram bot, openai api]
---

# 🌍 [AI Travel Planner] Tự động hóa kế hoạch du lịch với Telegram và OpenAI

[Các sếp đang mệt mỏi với việc lên kế hoạch du lịch thủ công? Hãy để n8n kết hợp với Telegram và OpenAI giúp các sếp tiết kiệm thời gian lên đến 80% cho các chuyến đi công tác. Workflow này sẽ tự động tìm kiếm vé máy bay, khách sạn và đưa ra đề xuất du lịch thông minh dựa trên yêu cầu của các sếp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên đến 80% cho việc lên kế hoạch du lịch
- Nhận được đề xuất du lịch cá nhân hóa và thông minh
- Tự động tìm kiếm vé máy bay và khách sạn từ nhiều nguồn
- Nhận thông báo qua Telegram ngay lập tức
- Hỗ trợ cả tiếng Việt và tiếng Anh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token
- API key từ OpenAI (hoặc DeepSeek)
- Tài khoản API cho các dịch vụ tìm kiếm vé máy bay và khách sạn (nếu sử dụng)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/3087)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, chọn "Import from JSON" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger** node:
   - Tạo bot mới trên Telegram và lấy bot token
   - Thêm bot vào nhóm chat hoặc kênh cần sử dụng
   - Cấu hình credentials với bot token

2. **OpenAI** nodes:
   - Tạo tài khoản OpenAI và lấy API key
   - Cấu hình credentials với API key
   - Chọn model phù hợp (gpt-3.5-turbo, gpt-4...)

3. **Search Flights** và **Search Hotels** nodes:
   - Cấu hình API endpoints cho các dịch vụ tìm kiếm vé máy bay và khách sạn
   - Thêm các headers và query parameters cần thiết

4. **Window Buffer Memory** node:
   - Điều chỉnh số lượng tin nhắn lưu trữ (k_window)
   - Cấu hình memory key phù hợp

5. **Business Travel Agent** node:
   - Cấu hình prompt cho agent du lịch
   - Thêm các tools cần thiết (search_flights, search_hotels...)

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu
2. Kiểm tra các kết quả từ các node
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack để nhận thông báo
2. Thêm node lưu log các yêu cầu du lịch
3. Tạo báo cáo định kỳ về các chuyến đi
4. Kết nối với Google Calendar để tự động tạo sự kiện

### 📌 Kết luận
[Workflow AI Travel Planner này sẽ giúp các sếp tiết kiệm thời gian đáng kể trong việc lên kế hoạch du lịch. Với khả năng tìm kiếm thông minh và đề xuất cá nhân hóa, các sếp có thể tập trung vào công việc quan trọng hơn. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!]