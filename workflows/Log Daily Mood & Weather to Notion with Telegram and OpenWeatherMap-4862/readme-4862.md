---
title: "🚀 Tự động ghi nhật ký tâm trạng và thời tiết hằng ngày lên Notion qua Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hỏi tâm trạng qua Telegram, lấy thông tin thời tiết từ OpenWeatherMap và lưu trữ gọn gàng vào Notion mỗi ngày."
slug: "tu-dong-ghi-nhat-ky-tam-trang-va-thoi-tiết-notion-telegram"
tags: [n8n, automation, no-code, notion, telegram, weather]
keywords: [n8n workflow, n8n telegram bot, notion automation, openweathermap n8n, n8n nhat ky tam trang]
---

# 🚀 Tự động ghi nhật ký tâm trạng và thời tiết hằng ngày lên Notion qua Telegram

Việc duy trì thói quen viết nhật ký (Journaling) mỗi ngày giúp chúng ta quản lý cảm xúc và nâng cao năng suất cá nhân rất tốt. Tuy nhiên, việc mở ứng dụng lên ghi chép thủ công đôi khi khiến các sếp dễ quên hoặc lười biếng. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa toàn bộ quy trình: mỗi ngày, hệ thống tự động gửi tin nhắn hỏi thăm tâm trạng qua Telegram, kết hợp gọi API lấy thông tin thời tiết thực tế, sau đó tự động tổng hợp và lưu trữ gọn gàng vào cơ sở dữ liệu Notion của các sếp mà không cần động tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn (100% No-Code):** Không cần nhớ lịch ghi nhật ký, bot Telegram sẽ chủ động "gõ cửa" các sếp mỗi ngày.
- **Tích hợp thông minh:** Kết hợp dữ liệu thời tiết thực tế (nhiệt độ, trạng thái trời) tại khu vực của các sếp cùng với tâm trạng thực tế lúc đó.
- **Lưu trữ khoa học:** Toàn bộ dữ liệu được đồng bộ hóa trực tiếp vào Notion, giúp việc theo dõi, tra cứu lịch sử cảm xúc qua các biểu đồ, bảng biểu trở nên dễ dàng.
- **Hoạt động 24/7:** Chạy ngầm ổn định trên hệ thống n8n tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
1. **Hệ thống n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Telegram & Telegram Bot Token** (tạo qua `@BotFather`).
3. **Tài khoản Notion & Notion Integration Token** cùng một Database mẫu để lưu nhật ký.
4. **API Key từ OpenWeatherMap** để lấy dữ liệu thời tiết (gói miễn phí là quá đủ dùng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow này, vào giao diện n8n Editor chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ cấu trúc nodes vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **Node `Daily Trigger` (cron):** Cấu hình lại mốc thời gian (giờ, phút) mà các sếp muốn bot Telegram bắt đầu gửi tin nhắn hỏi thăm tâm trạng hằng ngày.
- **Node `Send Mood Prompt` & `Wait for Mood Response` (telegram / telegramTrigger):** 
  - Kết nối với **Telegram Credentials** của bot do các sếp quản lý.
  - Thiết lập Chat ID của chính các sếp để bot biết gửi tin nhắn cho ai và nhận phản hồi từ ai.
- **Node `Get Weather using city name` / `Get Weather using lat/lon` (httpRequest):** 
  - Điền OpenWeatherMap API Key vào phần Header hoặc Query Parameters.
  - Cấu hình lại tên thành phố (`city`) hoặc tọa độ (`lat`/`lon`) nơi các sếp đang sinh sống để lấy đúng thông tin thời tiết.
- **Node `Retrieve Database` & `Add row into Notion` (notion):**
  - Kết nối với **Notion API Credentials**.
  - Trỏ đúng vào **Database ID** nơi lưu trữ nhật ký tâm trạng của các sếp. Đảm bảo các trường dữ liệu (Properties) trong Notion khớp với dữ liệu mà n8n gửi lên (như Ngày, Tâm trạng, Thời tiết, Nhiệt độ...).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử luồng chạy thủ công (gửi tin nhắn test qua Telegram và kiểm tra xem dữ liệu có đẩy lên Notion thành công không).
- Sau khi test ngon lành, gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ chạy tự động hằng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Telegram, các sếp có thể tích hợp thêm node **Slack** hoặc **Discord** để nhận thông báo hoặc gửi dữ liệu qua lại.
- **Ghi log lỗi:** Thêm node xử lý lỗi (Error Trigger) để nếu API thời tiết lỗi hoặc bot Telegram mất kết nối, hệ thống sẽ tự động bắn cảnh báo về một kênh riêng.
- **Thêm AI phân tích cảm xúc:** Tích hợp thêm các node LLM (OpenAI / Claude) để phân tích đoạn văn bản tâm trạng của các sếp và tự động đánh giá mức độ tích cực/tiêu cực (Sentiment Analysis) trước khi đẩy vào Notion.

### 📌 Kết luận
Một workflow cực kỳ thiết thực giúp số hóa thói quen ghi nhật ký cá nhân chỉ với vài bước cấu hình đơn giản. Chúc các sếp cài đặt thành công và có những trải nghiệm tuyệt vời cùng tự động hóa n8n!