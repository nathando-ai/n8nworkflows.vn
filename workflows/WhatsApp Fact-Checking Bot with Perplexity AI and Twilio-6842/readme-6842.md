---
title: "🚀 Bot Kiểm Tra Thông Tin qua WhatsApp với Perplexity AI & Twilio"
description: "Tự động kiểm tra tính chính xác của tin tức và trả lời ngay trên WhatsApp, giúp doanh nghiệp giảm thiểu rủi ro thông tin sai lệch."
slug: "bot-kiem-tra-thong-tin-qua-whatsapp-perplexity-ai-twilio"
tags: [n8n, automation, no-code, chatbot, ai, whatsapp]
keywords: [n8n workflow, tự động hóa, bot WhatsApp, Perplexity AI, Twilio, fact-checking]
---

# 🚀 Bot Kiểm Tra Thông Tin qua WhatsApp với Perplexity AI & Twilio

Bạn đang phải trả lời hàng trăm tin nhắn WhatsApp mỗi ngày, nhưng lo lắng về tính chính xác của thông tin? Đừng lo, workflow này sẽ giúp bạn tự động kiểm tra và trả lời ngay lập tức, 100% không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động trả lời ngay lập tức, không cần thao tác thủ công.
- **Chính xác cao**: Sử dụng Perplexity AI để kiểm tra nguồn tin, giảm rủi ro sai lệch.
- **Cá nhân hóa**: Mỗi tin nhắn được xử lý riêng, trả lời phù hợp với nội dung.
- **Hoạt động liên tục**: Workflow chạy 24/7, không bị gián đoạn.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Twilio Account SID** và **Auth Token** (để gửi/nhận tin WhatsApp).
- **Số điện thoại WhatsApp** (sandbox hoặc số chính thức) được đăng ký trên Twilio.
- **Perplexity AI API Key** (đăng ký tại https://perplexity.ai).
- **URL Webhook** của n8n (sẽ được cung cấp khi bạn import workflow).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow (đường dẫn: https://n8n.io/workflows/6842) hoặc copy toàn bộ JSON.
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách workflow.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| Webhook | `Webhook` | **HTTP Method**: POST, **Path**: `/whatsapp`, **Response**: 200 OK | Đảm bảo URL này được đăng ký với Twilio dưới dạng webhook cho inbound messages. |
| Perplexity | `Perplexity` | **API Key**: `PERPLEXITY_API_KEY`, **Prompt**: `Check the accuracy of the following text: {{ $json["body"] }}` | Thay `{{ $json["body"] }}` bằng trường chứa nội dung tin nhắn. |
| Twilio | `Twilio` | **Account SID**: `TWILIO_ACCOUNT_SID`, **Auth Token**: `TWILIO_AUTH_TOKEN`, **From**: `whatsapp:+<your_twilio_whatsapp_number>`, **To**: `whatsapp:+{{ $json["from"] }}` | `{{ $json["from"] }}` lấy số điện thoại người gửi. |
| StickyNote | `Sticky Note` | **Content**: `{{ $json["body"] }}` | Dùng để ghi chú debug, có thể bỏ qua. |

> **Lưu ý**: Mỗi node cần được gán **Credentials** tương ứng trong n8n. Vào **Credentials** → **New Credential** → chọn loại (Twilio, Perplexity, Webhook) và điền thông tin.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Node** trên node Webhook, nhập dữ liệu mẫu (ví dụ: `{"body":"Is the Eiffel Tower taller than 300m?"}`).
2. Kiểm tra output của node Perplexity và Twilio. Nếu trả lời đúng, workflow đã hoạt động.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram Notification**: Thêm node Slack/Telegram để nhận thông báo khi có tin nhắn mới hoặc khi có lỗi.
- **Lưu Log vào Google Sheets**: Dùng node Google Sheets để ghi lại lịch sử tin nhắn, câu trả lời, thời gian xử lý.
- **Scheduled Fact‑Check**: Thêm node Cron để tự động gửi câu hỏi kiểm tra định kỳ (ví dụ: “Check the latest news on X”).
- **Error Handling**: Thêm node Switch để phân loại lỗi (API key hết hạn, lỗi mạng) và gửi email cảnh báo.

## 📌 Kết luận

Workflow này giúp các sếp giảm tải công việc trả lời tin nhắn, đồng thời nâng cao độ tin cậy thông tin. Hãy triển khai ngay, trải nghiệm sự tự động hóa thông minh mà n8n mang lại!