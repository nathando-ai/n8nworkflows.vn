---
title: "🚀 Tự động hóa Chatbot AI với DeepSeek + Telegram + Bộ nhớ dài hạn"
description: "Hướng dẫn chi tiết cách xây dựng chatbot AI thông minh với DeepSeek, Telegram và bộ nhớ dài hạn bằng n8n. Giải phóng thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-hoa-chatbot-ai-deepseek-telegram-bo-nho-dai-han"
tags: [n8n, automation, no-code, AI, chatbot, Telegram, Google Docs]
keywords: [n8n workflow, tự động hóa, chatbot AI, DeepSeek, Telegram, bộ nhớ dài hạn]
---

# 🚀 Tự động hóa Chatbot AI với DeepSeek + Telegram + Bộ nhớ dài hạn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình tương tác khách hàng qua Telegram
- Ghi nhớ lịch sử hội thoại dài hạn thông qua Google Docs
- Tích hợp hai mô hình AI DeepSeek (chat và lý luận) để cung cấp các câu trả lời đa dạng và chính xác
- Tiết kiệm thời gian xử lý hàng nghìn tin nhắn mỗi ngày
- Nâng cao trải nghiệm khách hàng với các câu trả lời nhanh chóng và liên tục
- Tự động lưu trữ và truy xuất thông tin quan trọng từ các cuộc hội thoại trước đó
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token từ BotFather
- Tài khoản Google và quyền truy cập Google Docs
- API key từ DeepSeek AI
- URL endpoint để thiết lập webhook (cần phải có SSL/TLS)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/2864`
4. Nhấn "Import" để tải workflow vào editor

Hoặc bạn có thể:
1. Truy cập link workflow: https://n8n.io/workflows/2864
2. Nhấn nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, nhấn vào nút "Import from Clipboard"
4. Dán JSON đã sao chép và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Listen for Telegram Events** (Webhook node):
   - Thiết lập path cho webhook (ví dụ: "/wbot")
   - Đảm bảo URL của bạn có SSL/TLS (bắt buộc cho Telegram webhook)
   - Thiết lập webhook với Telegram bằng cách gọi API:
     ```
     https://api.telegram.org/bot{your_bot_token}/setWebhook?url={your_webhook_url}
     ```

2. **Telegram Response** và **Error message** nodes:
   - Cấu hình credentials "telegramApi" với bot token của bạn
   - Đảm bảo bot có quyền gửi tin nhắn đến người dùng

3. **DeepSeek-R1 Reasoning** và **DeepSeek-V3 Chat** nodes:
   - Cấu hình credentials "openAiApi" với API key từ DeepSeek
   - Đảm bảo bạn đã đăng ký tài khoản và nhận được API key từ DeepSeek
   - Base URL: `https://api.deepseek.com`

4. **Save Long Term Memories** và **Retrieve Long Term Memories** nodes:
   - Cấu hình credentials "googleDocsOAuth2Api"
   - Tạo một Google Doc để lưu trữ bộ nhớ dài hạn
   - Chia sẻ Google Doc với tài khoản dịch vụ của bạn
   - Cập nhật ID của Google Doc trong các node tương ứng

5. **Window Buffer Memory** node:
   - Thiết lập kích thước bộ nhớ (số lượng tin nhắn lưu trữ)
   - Điều chỉnh theo nhu cầu của bạn (mặc định thường là 5-10 tin nhắn)

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu bằng cách gửi một tin nhắn thử đến bot Telegram của bạn.
- Kiểm tra các node để đảm bảo dữ liệu được truyền đúng cách.
- Bật Active workflow sau khi đã kiểm tra và cấu hình đầy đủ.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Discord để nhận thông báo khi có tin nhắn mới
- Thêm node để gửi báo cáo hàng ngày về số lượng tin nhắn đã xử lý
- Tích hợp với hệ thống CRM để lưu trữ thông tin khách hàng
- Thêm node để xử lý các lệnh đặc biệt (ví dụ: /help, /status)
- Tối ưu hóa bộ nhớ dài hạn bằng cách thêm phân loại thông tin quan trọng

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa chatbot AI với DeepSeek, Telegram và bộ nhớ dài hạn. Bằng cách triển khai workflow này, các sếp có thể tiết kiệm thời gian đáng kể, nâng cao trải nghiệm khách hàng và tự động hóa hoàn toàn quá trình tương tác khách hàng. Hãy thử ngay và trải nghiệm sức mạnh của tự động hóa AI!