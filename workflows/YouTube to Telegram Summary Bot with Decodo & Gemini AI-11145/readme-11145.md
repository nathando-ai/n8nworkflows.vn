---
title: "🎥 [Tự động hóa] YouTube to Telegram Summary Bot với Decodo & Gemini AI - Tiết kiệm thời gian xem video"
description: "Workflow n8n tự động hóa chuyển đổi nội dung video YouTube thành tóm tắt ngắn gọn qua Telegram, giúp tiết kiệm thời gian xem và hiểu nội dung nhanh chóng."
slug: "tu-dong-hoa-youtube-telegram-summary-bot"
tags: [n8n, automation, no-code, AI, content-creation, telegram]
keywords: [n8n workflow, tự động hóa, tóm tắt video, AI summarization, Telegram bot]
---

# 🎥 [Tự động hóa] YouTube to Telegram Summary Bot với Decodo & Gemini AI

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xem những video dài hơi trên YouTube mà không có thời gian? Workflow này sẽ giúp các sếp tự động hóa quá trình chuyển đổi nội dung video thành tóm tắt ngắn gọn qua Telegram, tiết kiệm thời gian và giúp hiểu nội dung nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xem video: Chuyển đổi nội dung video dài thành tóm tắt ngắn gọn.
- Tăng hiệu quả làm việc: Nhận thông tin quan trọng từ video mà không cần xem toàn bộ.
- Cá nhân hóa nội dung: Tóm tắt được điều chỉnh theo nhu cầu của từng người dùng.
- Hoạt động liên tục: Tự động xử lý và gửi tóm tắt ngay khi nhận được liên kết video.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và một bot Telegram.
- API key từ Decodo để lấy nội dung video.
- API key từ Google Gemini để xử lý tóm tắt.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/11145](https://n8n.io/workflows/11145).
3. Hoặc tải file JSON từ liên kết trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "On New Message"**: Cấu hình Telegram API credentials để bot có thể nhận tin nhắn.
- **Node "Decodo Youtube Transcript Scrapper" và "Decodo Youtube Metadata Scrapper"**: Cấu hình HTTP Header Auth credentials với API key từ Decodo.
- **Node "Gemini 3.0"**: Cấu hình Google Palm API credentials để sử dụng mô hình Gemini.
- **Node "Generate TLDR"**: Điều chỉnh prompt nếu cần thay đổi cách tóm tắt nội dung.
- **Node "Send Summary Part"**: Cấu hình Telegram API credentials để bot có thể gửi tin nhắn.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo tóm tắt.
- Lưu log các tóm tắt đã gửi để tham khảo sau.
- Gửi báo cáo định kỳ về các video đã tóm tắt.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tăng hiệu quả làm việc bằng cách tự động hóa quá trình tóm tắt nội dung video. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!