---
title: "🎙️ Tự động hóa chuyển đổi giọng nói thành văn bản với Google Gemini và Telegram"
description: "Hướng dẫn tự động hóa chuyển đổi giọng nói thành văn bản sử dụng Google Gemini và Telegram, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-chuyen-doi-giong-noi-thanh-van-ban-voi-google-gemini-va-telegram"
tags: [n8n, automation, no-code, AI, Google, Telegram]
keywords: [n8n workflow, tự động hóa, Google Gemini, chuyển đổi giọng nói, Telegram]
---

# 🎙️ Tự động hóa chuyển đổi giọng nói thành văn bản với Google Gemini và Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc chuyển đổi giọng nói thành văn bản.
- Tự động hóa toàn bộ quy trình xử lý file âm thanh.
- Tích hợp dễ dàng với các công cụ khác thông qua webhook.
- Hỗ trợ xử lý nhiều định dạng file âm thanh khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini.
- Tài khoản Telegram và bot token.
- Google Drive API key (nếu sử dụng tính năng tải file từ Google Drive).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/3388](https://n8n.io/workflows/3388) để tải file JSON.
2. Mở n8n Editor và chọn "Import from File" hoặc "Import from URL".
3. Chọn file JSON đã tải về và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Telegram Trigger1**: Cấu hình bot token và chat ID để nhận tin nhắn từ Telegram.
- **initialize upload session**: Cấu hình API key cho Google Gemini.
- **Upload file**: Cấu hình API key cho Google Drive (nếu sử dụng).
- **Ask Gemini to transcribe**: Cấu hình prompt và tham số cho Google Gemini.
- **Reply in Telegram**: Cấu hình bot token và chat ID để gửi tin nhắn trả lời.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi quá trình chuyển đổi hoàn tất.
- Lưu log các file đã xử lý vào Google Sheets để theo dõi.
- Tự động gửi báo cáo định kỳ về số lượng file đã xử lý và thời gian trung bình.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc chuyển đổi giọng nói thành văn bản. Với tính năng tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào các công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!