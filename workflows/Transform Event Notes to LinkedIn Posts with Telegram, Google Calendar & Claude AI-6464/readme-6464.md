---
title: "🚀 Tự động hóa LinkedIn Posts từ Ghi chú Sự kiện qua Telegram + Google Calendar + AI Claude"
description: "Hướng dẫn tự động hóa việc chuyển đổi ghi chú sự kiện thành bài đăng LinkedIn chuyên nghiệp bằng Telegram, Google Calendar và AI Claude - tiết kiệm thời gian và nâng cao hiệu quả mạng xã hội"
slug: "tu-dong-hoa-linkedin-posts-tu-ghi-chu-su-kien"
tags: [n8n, automation, no-code, linkedin, google-calendar]
keywords: [n8n workflow, tự động hóa, linkedin, google calendar, ai claude]
---

# 🚀 Tự động hóa LinkedIn Posts từ Ghi chú Sự kiện qua Telegram + Google Calendar + AI Claude

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải viết bài đăng LinkedIn sau mỗi sự kiện? Với workflow này, các sếp có thể chuyển đổi nhanh chóng ghi chú sự kiện thành bài đăng LinkedIn chuyên nghiệp chỉ với một tin nhắn Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian viết bài đăng: Chỉ cần gửi tin nhắn Telegram, hệ thống tự động xử lý
- Bài đăng chuyên nghiệp: AI Claude tạo nội dung chất lượng với hashtag phù hợp
- Lưu trữ dữ liệu: Tất cả thông tin sự kiện và bài đăng được lưu trữ trong Supabase
- Tích hợp đa nền tảng: Kết nối liền mạch giữa Telegram, Google Calendar và LinkedIn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot (tạo qua @BotFather)
- Quyền truy cập Google Calendar API (OAuth2 credentials)
- API key của Anthropic (để sử dụng Claude)
- Tài khoản Supabase (để lưu trữ dữ liệu)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6464](https://n8n.io/workflows/6464)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất

Hoặc có thể copy JSON workflow và paste vào Editor của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**: Cần cấu hình credentials cho Telegram API
   - Đi đến "Credentials" trong n8n
   - Tạo mới "Telegram API" và điền thông tin bot token
   - Lưu credentials này vào node "Telegram Trigger"

2. **Google Calendar**: Cấu hình credentials cho Google Calendar API
   - Tạo mới "Google Calendar OAuth2 API" trong credentials
   - Điền thông tin client ID và client secret từ Google Cloud Console
   - Lưu credentials này vào node "Search for Google Calendar"

3. **Anthropic Chat Model**: Cấu hình API key cho Claude
   - Tạo mới "Anthropic API" trong credentials
   - Điền API key từ tài khoản Anthropic
   - Lưu credentials này vào node "Anthropic Chat Model"

4. **Supabase**: Cấu hình kết nối đến database
   - Tạo mới "Supabase API" trong credentials
   - Điền thông tin URL và API key từ Supabase
   - Lưu credentials này vào node "Save to Supabase"

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra các node quan trọng:
   - Xác nhận Telegram bot nhận tin nhắn
   - Kiểm tra Google Calendar trả về sự kiện đúng
   - Đảm bảo AI Claude tạo bài đăng phù hợp
   - Xác nhận dữ liệu được lưu đúng trong Supabase
3. Bật Active workflow để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
1. Tùy chỉnh prompt cho AI Claude: Chỉnh sửa node "Format the matched event" để điều chỉnh style viết bài
2. Thêm thông báo Slack: Kết nối thêm node Slack để nhận thông báo khi có bài đăng mới
3. Tự động đăng LinkedIn: Kết nối với node LinkedIn để tự động đăng bài
4. Thêm phân tích cảm xúc: Sử dụng node AI để phân tích cảm xúc từ ghi chú sự kiện

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian viết bài đăng LinkedIn sau mỗi sự kiện, đồng thời tạo ra nội dung chuyên nghiệp với AI. Hãy thử ngay và nâng cao hiệu quả mạng xã hội của bạn!