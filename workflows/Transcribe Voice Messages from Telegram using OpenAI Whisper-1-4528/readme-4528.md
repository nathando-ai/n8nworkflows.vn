---
title: "🎤 Tự động chuyển đổi tin nhắn thoại Telegram thành văn bản với OpenAI Whisper-1"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi tin nhắn thoại Telegram thành văn bản sử dụng công nghệ AI Whisper-1 của OpenAI, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-chuyen-doi-tin-nhan-thoai-telegram-thanh-van-ban-openai-whisper-1"
tags: [n8n, automation, no-code, telegram, openai]
keywords: [n8n workflow, tự động hóa, telegram, openai whisper, chuyển đổi âm thanh thành văn bản]
---

# 🎤 Tự động chuyển đổi tin nhắn thoại Telegram thành văn bản với OpenAI Whisper-1

[Các sếp đang gặp khó khăn khi phải nghe lại các tin nhắn thoại trên Telegram để lấy thông tin quan trọng. Quá trình này tốn thời gian và dễ gây lỗi. Workflow này giúp tự động hóa toàn bộ quy trình từ nhận tin nhắn thoại đến chuyển đổi thành văn bản sử dụng công nghệ AI Whisper-1 của OpenAI, đảm bảo chính xác và tiết kiệm thời gian.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi tin nhắn thoại thành văn bản ngay lập tức.
- Tiết kiệm thời gian đáng kể so với việc nghe lại từng tin nhắn.
- Dữ liệu được xử lý chính xác và không bị mất mát thông tin.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và quyền truy cập vào bot Telegram.
- API Key của OpenAI để sử dụng dịch vụ Whisper-1.
- Tài khoản n8n đã được cài đặt và cấu hình sẵn sàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/4528](https://n8n.io/workflows/4528).
2. Nhấp vào nút "Download" để tải file JSON của workflow.
3. Trong giao diện n8n, nhấp vào "Import from File" và chọn file JSON vừa tải về.

Hoặc, các sếp cũng có thể copy/paste JSON sau đây vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "resource": "file"
      },
      "name": "Get audio file",
      "type": "telegram",
      "typeVersion": 1,
      "position": [
        110,
        300
      ]
    },
    {
      "parameters": {
        "operation": "transcribe",
        "resource": "audio"
      },
      "name": "Transcribe audio",
      "type": "openAi",
      "typeVersion": 1,
      "position": [
        410,
        300
      ]
    },
    {
      "parameters": {},
      "name": "Message Trigger",
      "type": "telegramTrigger",
      "typeVersion": 1,
      "position": [
        -190,
        300
      ]
    },
    {
      "parameters": {},
      "name": "Send transcription message",
      "type": "telegram",
      "typeVersion": 1,
      "position": [
        610,
        300
      ]
    },
    {
      "parameters": {},
      "name": "Route Chat Input",
      "type": "switch",
      "typeVersion": 1,
      "position": [
        -190,
        460
      ]
    }
  ],
  "connections": {
    "Message Trigger": {
      "main": [
        [
          {
            "node": "Route Chat Input",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Route Chat Input": {
      "main": [
        [
          {
            "node": "Get audio file",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get audio file": {
      "main": [
        [
          {
            "node": "Transcribe audio",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Transcribe audio": {
      "main": [
        [
          {
            "node": "Send transcription message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node sau:

- **Message Trigger**: Cấu hình để nhận tin nhắn từ Telegram. Các sếp cần cung cấp thông tin về bot Telegram và kênh chat.
- **Route Chat Input**: Cấu hình để lọc và định tuyến tin nhắn. Các sếp có thể thêm các điều kiện để chỉ xử lý các tin nhắn thoại.
- **Get audio file**: Cấu hình để tải file âm thanh từ tin nhắn Telegram. Các sếp cần cung cấp thông tin về tài khoản Telegram và quyền truy cập.
- **Transcribe audio**: Cấu hình để chuyển đổi âm thanh thành văn bản sử dụng OpenAI Whisper-1. Các sếp cần cung cấp API Key của OpenAI.
- **Send transcription message**: Cấu hình để gửi kết quả chuyển đổi văn bản về Telegram. Các sếp cần cung cấp thông tin về bot Telegram và kênh chat.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Nhấp vào nút "Execute Workflow" để kiểm tra dữ liệu mẫu.
2. Kiểm tra kết quả chuyển đổi văn bản trên Telegram.
3. Nếu mọi thứ hoạt động tốt, các sếp có thể bật chế độ "Active" để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với các dịch vụ khác như Slack hoặc Email để gửi kết quả chuyển đổi văn bản đến các kênh khác.
- Các sếp có thể lưu log các kết quả chuyển đổi để theo dõi và phân tích sau này.
- Các sếp có thể gửi báo cáo định kỳ về số lượng tin nhắn đã xử lý và thời gian trung bình để chuyển đổi.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình chuyển đổi tin nhắn thoại thành văn bản, tiết kiệm thời gian và nâng cao hiệu suất làm việc. Các sếp chỉ cần cấu hình một lần và workflow sẽ chạy liên tục mà không cần can thiệp thủ công. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!