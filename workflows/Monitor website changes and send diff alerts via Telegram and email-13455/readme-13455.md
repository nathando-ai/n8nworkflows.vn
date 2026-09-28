---
title: "🚀 Tự động theo dõi thay đổi website & gửi cảnh báo qua Telegram, Email với n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động quét website, phát hiện thay đổi nội dung (diff) và gửi cảnh báo tức thì qua Telegram và Email mà không cần code."
slug: "tu-dong-theo-doi-thay-doi-website-n8n"
tags: [n8n, automation, no-code, web-monitoring, telegram-bot, google-sheets]
keywords: [n8n workflow, theo dõi thay đổi website, website change monitor, cảnh báo telegram n8n, tự động hóa no-code]
---

# 🚀 Tự động theo dõi thay đổi website & gửi cảnh báo qua Telegram, Email với n8n

Việc thủ công kiểm tra các trang web của đối thủ, cập nhật giá sản phẩm, thay đổi chính sách hay thông tin tuyển dụng mỗi ngày thực sự tốn rất nhiều thời gian và dễ bỏ sót. Các sếp có đang gặp tình trạng này không?

Giải pháp ở đây chính là **workflow n8n tự động hóa 100%**: Hệ thống sẽ tự động quét website định kỳ, lọc sạch nội dung, so sánh sự khác biệt (line-by-line diff) với phiên bản trước đó và bắn tin nhắn cảnh báo ngay lập tức qua Telegram và Email khi có bất kỳ thay đổi nào xuất hiện!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt trọn thay đổi tức thì**: Không bỏ lỡ bất kỳ biến động giá cả, chính sách hay nội dung nào từ đối thủ hoặc hệ thống quan trọng.
- **Tiết kiệm 10+ giờ mỗi tuần**: Thay vì F5 trình duyệt liên tục, để n8n làm thay việc đó 24/7.
- **Thông minh & không nhiễu**: Chỉ gửi cảnh báo khi nội dung thực sự thay đổi, kèm theo tóm tắt mức độ nghiêm trọng (severity) và phần trăm thay đổi.
- **Đa kênh tiếp nhận**: Nhận thông báo nhanh chóng qua Telegram cá nhân/nhóm và Email chi tiết.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets**: Tài khoản Google để làm cơ sở dữ liệu lưu snapshot lịch sử website.
- **Telegram Bot**: Tạo một bot thông qua `@BotFather` để lấy `Bot Token` và `Chat ID`.
- **Email/SMTP**: Tài khoản SMTP hoặc Gmail để gửi cảnh báo qua email (tùy chọn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy JSON của workflow gốc hoặc tải file về, sau đó chọn **Import from File** hoặc dán trực tiếp vào n8n Editor của mình. Workflow bao gồm **12 nodes** được tối ưu hóa mượt mà.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình các node quan trọng sau:

- **⏰ Every 4 Hours (`scheduleTrigger`)**: 
  - Quy định tần suất quét website. Các sếp có thể đổi thành mỗi giờ (1 hour) cho các trang quan trọng hoặc mỗi ngày (24 hours) cho các trang ít biến động.
- **📋 URL List (`code`)**: 
  - Chỉnh sửa node này để thêm danh sách các website cần theo dõi. Thêm mỗi mục (item) gồm `name` (tên gợi nhớ) và `url` (đường dẫn đầy đủ).
- **📋 Load Previous Snapshot & 💾 Save Snapshot (`googleSheets`)**: 
  - Tạo một Google Sheet mới với các cột: `Name`, `url`, `selector`, `pageTitle`, `metaDescription`, `cleanText`, `contentHash`, `contentLength`, `fetchedAt`, `httpStatus`.
  - Kết nối tài khoản Google OAuth và điền **Spreadsheet ID** vào cả 2 node đọc/ghi Google Sheets trong workflow.
- **📲 Telegram Alert (`telegram`)**: 
  - Thêm Telegram Credential (`Bot Token`) và cấu hình `Chat ID` nơi nhận thông báo.
- **📧 Email Alert (`emailSend`)**: 
  - Cấu hình SMTP hoặc tài khoản Gmail để gửi email cảnh báo chi tiết.

#### 3. Kích hoạt ⚡️
- **Chạy thử lần đầu (First Run = Baseline)**: Ở lần chạy đầu tiên, hệ thống sẽ lưu lại snapshot làm mốc so sánh (baseline) mà **chưa gửi cảnh báo vội** nhằm tránh spam. Thay đổi sẽ bắt đầu được phát hiện từ lần chạy thứ 2 trở đi.
- Sau khi test thủ công thành công, các sếp gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh CSS Selector**: Thêm từ khóa selector trong danh sách URL để chỉ theo dõi đúng vùng nội dung quan trọng trên trang (ví dụ: bảng giá sản phẩm, phần thông báo tuyển dụng).
- **Mở rộng kênh nhận tin**: Có thể tích hợp thêm các node **Slack**, **Discord** hoặc **WhatsApp** để gửi thông báo cho cả team cùng nắm bắt.
- **Tích hợp Trợ lý AI**: Thay vì hiển thị diff thô, các sếp có thể gắn thêm node OpenAI hoặc Ollama để AI tóm tắt ngắn gọn sự thay đổi dưới dạng văn bản dễ hiểu.

### 📌 Kết luận
Workflow **Monitor website changes and send diff alerts** là trợ thủ đắc lực giúp các sếp tự động hóa hoàn toàn công tác nghiên cứu thị trường, theo dõi đối thủ và quản trị thông tin website. Hãy cài đặt ngay để tối ưu hóa thời gian và gia tăng lợi thế cạnh tranh cho doanh nghiệp!