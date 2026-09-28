---
title: "🚀 Tự động phân loại email Gmail và gửi cảnh báo ưu tiên qua Gemini AI và Telegram"
description: "Workflow n8n tự động hóa phân loại email Gmail, sử dụng AI Gemini để phân tích và gửi cảnh báo ưu tiên qua Telegram, giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-phan-loai-email-gmail-voi-gemini-telegram"
tags: [n8n, automation, no-code, email, telegram, ai]
keywords: [n8n workflow, tự động hóa email, Gemini AI, Telegram, phân loại email]
---

# 🚀 Tự động phân loại email Gmail và gửi cảnh báo ưu tiên qua Gemini AI và Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải đối mặt với hàng loạt email hàng ngày, nhưng không phải tất cả đều quan trọng. Việc phải đọc và phân loại thủ công các email này không chỉ tốn thời gian mà còn dễ bỏ sót những thông tin quan trọng. Workflow này sẽ giúp các sếp tự động hóa quy trình này, sử dụng sức mạnh của AI Gemini để phân tích và gửi cảnh báo ưu tiên qua Telegram, đảm bảo không bỏ sót bất kỳ thông tin quan trọng nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân loại và xử lý email mà không cần can thiệp thủ công.
- **Chính xác cao**: Sử dụng AI Gemini để phân tích và đánh giá mức độ ưu tiên của email.
- **Thông báo tức thì**: Gửi cảnh báo ưu tiên qua Telegram ngay lập tức, đảm bảo không bỏ sót thông tin quan trọng.
- **Dễ dàng tùy chỉnh**: Đơn giản hóa quy trình bằng cách chỉ cần cập nhật một số biến trong node `Set Context`.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail và quyền truy cập OAuth2.
- API Key của Google Gemini.
- Bot Telegram và Chat ID để nhận cảnh báo.
- Tạo một n8n Data Table với schema phù hợp và lưu lại ID của bảng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/16032](https://n8n.io/workflows/16032).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Gmail Trigger**: Cấu hình credentials Google API để kết nối với Gmail.
- **Set Context**: Cập nhật các biến như `data_table_id`, `owner_name`, `owner_email`, và `chatId` của Telegram.
- **Google Gemini Flash**: Cấu hình credentials Google Palm API để sử dụng AI Gemini.
- **Notify via Telegram (High Priority)**: Cập nhật credentials Telegram API để gửi cảnh báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thay đổi node Telegram thành Slack để nhận cảnh báo trên Slack.
- **Lưu log chi tiết**: Thêm node để lưu log chi tiết vào Google Sheets hoặc cơ sở dữ liệu.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp hàng ngày qua email hoặc Telegram.
- **Tùy chỉnh AI**: Chỉnh sửa `systemMessage` trong node `AI Email Analyzer` để thay đổi cách AI đánh giá mức độ ưu tiên và phân loại email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình phân loại email, sử dụng AI Gemini để phân tích và gửi cảnh báo ưu tiên qua Telegram. Với việc chỉ cần cấu hình một số biến và kích hoạt workflow, các sếp có thể tiết kiệm thời gian và đảm bảo không bỏ sót bất kỳ thông tin quan trọng nào. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của mình!