---
title: "🚀 Tự động phân loại ticket hỗ trợ bằng AI GPT-4o và gửi đến Slack"
description: "Giải pháp tự động hóa 100% không cần code giúp phân loại ticket hỗ trợ theo mức độ cảm xúc và gửi đến kênh Slack phù hợp, tiết kiệm thời gian xử lý và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-phan-loai-ticket-ho-tro-bang-ai-gpt-4o-va-gui-den-slack"
tags: [n8n, automation, no-code, ticket-management, ai]
keywords: [n8n workflow, tự động hóa ticket, phân loại cảm xúc, Slack integration, AI hỗ trợ khách hàng]
---

# 🚀 Tự động phân loại ticket hỗ trợ bằng AI GPT-4o và gửi đến Slack

[Các sếp đang gặp khó khăn khi phải xử lý hàng nghìn ticket hỗ trợ hàng ngày một cách thủ công. Với workflow này, các sếp có thể tự động phân loại ticket theo mức độ cảm xúc của khách hàng và gửi đến các kênh Slack phù hợp, giúp tiết kiệm thời gian và cải thiện trải nghiệm khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý ticket: Tự động phân loại ticket theo mức độ cảm xúc của khách hàng.
- Cải thiện trải nghiệm khách hàng: Gửi ticket đến các kênh Slack phù hợp, giúp đội ngũ hỗ trợ phản hồi nhanh chóng.
- Tăng hiệu quả làm việc: Giảm thời gian xử lý thủ công và tập trung vào các ticket quan trọng.
- Tự động hóa hoàn toàn: Không cần lập trình, chỉ cần cấu hình các thông số cơ bản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI để sử dụng GPT-4o cho phân tích cảm xúc.
- Tài khoản Slack để gửi ticket đến các kênh phù hợp.
- URL endpoint để nhận ticket hỗ trợ (có thể là từ hệ thống CRM hoặc form liên hệ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút "Import from URL" và dán link sau vào ô nhập liệu: `https://n8n.io/workflows/15304`.
3. Hoặc, các sếp có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node sau:

- **When Ticket Received (Webhook)**: Cấu hình URL endpoint để nhận ticket hỗ trợ. Ví dụ: `https://your-n8n-instance.com/webhook/support-ticket`.
- **OpenAI Sentiment Analysis**: Cấu hình credentials cho OpenAI và điền prompt để phân tích cảm xúc. Ví dụ:
  ```json
  {
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant that analyzes customer support tickets and determines the sentiment score from 1 to 10, where 1 is very negative and 10 is very positive."
      },
      {
        "role": "user",
        "content": "Analyze the sentiment of this support ticket: {{ $node["Normalize Ticket Data"].json["ticketContent"] }}"
      }
    ]
  }
  ```
- **Send to Slack #escalation, #support, #feedback**: Cấu hình credentials cho Slack và điền tên kênh Slack để gửi ticket. Ví dụ:
  ```json
  {
    "channel": "#escalation",
    "text": "Ticket from {{ $node["Normalize Ticket Data"].json["customerName"] }}: {{ $node["Normalize Ticket Data"].json["ticketContent"] }}"
  }
  ```

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần thực hiện các bước sau:

1. Test run workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể tùy chỉnh logic phân loại ticket dựa trên các tiêu chí khác ngoài cảm xúc, như mức độ ưu tiên, loại ticket, v.v.
- Kết hợp với Slack để nhận thông báo khi ticket được gửi đến các kênh khác nhau.
- Lưu log các ticket đã được xử lý để theo dõi và phân tích hiệu suất hỗ trợ khách hàng.
- Gửi báo cáo định kỳ về số lượng ticket đã được xử lý và mức độ cảm xúc trung bình của khách hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động phân loại ticket hỗ trợ theo mức độ cảm xúc của khách hàng và gửi đến các kênh Slack phù hợp, tiết kiệm thời gian và cải thiện trải nghiệm khách hàng. Các sếp chỉ cần cấu hình các thông số cơ bản và kích hoạt workflow để bắt đầu tự động hóa quy trình.