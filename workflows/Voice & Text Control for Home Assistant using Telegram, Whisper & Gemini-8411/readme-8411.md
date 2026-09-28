---
title: "🤖 Tự động hóa Home Assistant bằng Telegram, Whisper & Gemini - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động hóa điều khiển Home Assistant thông qua Telegram bằng công nghệ chuyển giọng nói thành văn bản (Whisper) và trí tuệ nhân tạo (Gemini) - không cần code"
slug: "tu-dong-hoa-home-assistant-bang-telegram-whisper-gemini"
tags: [n8n, automation, no-code, home-assistant, ai-chatbot]
keywords: [n8n workflow, tự động hóa, home assistant, telegram, whisper, gemini]
---

# 🤖 Tự động hóa Home Assistant bằng Telegram, Whisper & Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi điều khiển thiết bị thông minh bằng giọng nói hoặc văn bản thông qua Telegram. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Điều khiển thiết bị thông minh bằng giọng nói hoặc văn bản qua Telegram
- **Trí tuệ nhân tạo**: Hiểu ý định người dùng thông qua Google Gemini
- **Tương thích đa kênh**: Hoạt động đồng thời với n8n Chat và Telegram
- **Giao diện đẹp mắt**: Tự động định dạng tin nhắn với markdown/HTML
- **Bộ nhớ ngắn hạn**: Giữ trạng thái hội thoại để hiểu ngữ cảnh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- API Key từ OpenAI (cho Whisper)
- API Key từ Google (cho Gemini)
- Tài khoản Home Assistant và token truy cập
- Tài khoản n8n (nếu sử dụng n8n Chat)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/8411)
2. Click "Import" và chọn "Import from URL"
3. Dán link workflow vào và hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger** và **Telegram Send**:
   - Tạo credentials mới trong n8n với tên "telegramApi"
   - Điền Bot Token và Chat ID của bạn
   - Lưu ý: Chat ID phải là số (không phải tên người dùng)

2. **Speech to Text** (Whisper):
   - Tạo credentials "openAiApi" với API Key từ OpenAI
   - Chọn model "whisper-1" hoặc phiên bản mới nhất

3. **Google Gemini Chat Model**:
   - Tạo credentials "googlePalmApi" với API Key từ Google
   - Chọn model "gemini-pro" hoặc phiên bản mới nhất

4. **Home Assistant Connector**:
   - Tạo credentials "httpBearerAuth" với URL Home Assistant và token truy cập
   - URL thường dạng: `http://<địa-chỉ-ip-của-home-assistant>:8123/api`

5. **When chat message received**:
   - Nếu sử dụng n8n Chat, cần cấu hình webhook để nhận tin nhắn

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi tin nhắn thử nghiệm qua Telegram hoặc n8n Chat
   - Kiểm tra từng node để đảm bảo dữ liệu truyền đúng
2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Teams**: Thêm node để nhận tin nhắn từ các nền tảng khác
- **Lưu log hoạt động**: Thêm node để lưu nhật ký các lệnh được thực thi
- **Tạo báo cáo định kỳ**: Thêm node để gửi báo cáo trạng thái thiết bị hàng ngày
- **Mở rộng chức năng**: Thêm các công cụ khác như Google Calendar, Weather API...

### 📌 Kết luận
Workflow này mang đến giải pháp toàn diện để điều khiển Home Assistant thông qua giao diện thân thiện của Telegram, kết hợp sức mạnh của trí tuệ nhân tạo và chuyển giọng nói thành văn bản. Với thiết kế mô-đun, các sếp có thể dễ dàng mở rộng và tùy chỉnh theo nhu cầu cụ thể của mình. Hãy thử ngay và tự động hóa cuộc sống thông minh của bạn!