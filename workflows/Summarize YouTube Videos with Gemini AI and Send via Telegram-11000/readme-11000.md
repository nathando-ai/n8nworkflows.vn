---
title: "🎬 Tóm tắt video YouTube bằng AI Gemini và gửi qua Telegram - Workflow n8n"
description: "Tự động hóa việc tóm tắt video YouTube bằng AI Gemini và gửi kết quả qua Telegram. Tiết kiệm thời gian xem video, nhận thông tin nhanh chóng và chính xác."
slug: "tom-tat-video-youtube-bang-ai-gemini-va-gui-qua-telegram"
tags: [n8n, automation, no-code, AI, Telegram]
keywords: [n8n workflow, tự động hóa, tóm tắt video, AI Gemini, Telegram]
---

# 🎬 Tóm tắt video YouTube bằng AI Gemini và gửi qua Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ cảm thấy mệt mỏi khi phải xem những video dài trên YouTube? Với workflow này, các sếp có thể tự động hóa việc tóm tắt nội dung video bằng AI Gemini và nhận kết quả ngay trên Telegram. Không cần phải tốn thời gian xem video dài, các sếp có thể nhanh chóng nắm bắt thông tin quan trọng từ video mà không cần phải đọc toàn bộ nội dung.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xem video: Các sếp không cần phải tốn thời gian xem video dài, mà có thể nhận thông tin quan trọng một cách nhanh chóng.
- Nhận thông tin chính xác: AI Gemini sẽ tóm tắt nội dung video một cách chính xác và chi tiết, giúp các sếp nắm bắt thông tin quan trọng.
- Cá nhân hóa: Các sếp có thể tùy chỉnh ngôn ngữ và cách thức tóm tắt để phù hợp với nhu cầu của mình.
- Hoạt động liên tục: Workflow có thể chạy 24/7, giúp các sếp nhận thông tin bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram.
- API key từ Decodo để lấy dữ liệu video.
- API key từ Google Gemini để tóm tắt nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **On New Message**: Cấu hình Telegram API để nhận tin nhắn từ người dùng.
- **Decodo Youtube Transcript Scrapper**: Cấu hình HTTP Header Auth với API key từ Decodo.
- **Gemini Flash**: Cấu hình Google Palm API với API key từ Google Gemini.
- **Send Summary Part**: Cấu hình Telegram API để gửi kết quả tóm tắt về cho người dùng.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể tùy chỉnh ngôn ngữ tóm tắt bằng cách thay đổi tham số `languageCode` trong node **Set: Video ID & Config**.
- Để nhận thông báo lỗi, các sếp có thể cấu hình node **Alert Admin** để gửi thông báo lỗi về cho người quản trị.
- Các sếp có thể kết hợp với các công cụ khác như Slack hoặc Email để nhận kết quả tóm tắt.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nhận thông tin chính xác từ video YouTube một cách nhanh chóng. Với AI Gemini và Telegram, các sếp có thể tự động hóa việc tóm tắt nội dung video và nhận kết quả một cách dễ dàng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của mình!