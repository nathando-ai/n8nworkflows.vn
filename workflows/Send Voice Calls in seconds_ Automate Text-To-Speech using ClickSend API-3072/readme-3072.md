---
title: "📞 Tự động hóa cuộc gọi thoại bằng Text-to-Speech với ClickSend API"
description: "Hướng dẫn tự động hóa cuộc gọi thoại bằng Text-to-Speech với n8n và ClickSend API. Giải pháp hoàn hảo cho thông báo, nhắc nhở và giao tiếp thoại tự động."
slug: "tu-dong-hoa-cuoc-goi-thoai-text-to-speech-clicksend-api"
tags: [n8n, automation, no-code, voice-call, text-to-speech]
keywords: [n8n workflow, tự động hóa cuộc gọi thoại, text-to-speech, ClickSend API, tự động hóa không cần code]
---

# 📞 Tự động hóa cuộc gọi thoại bằng Text-to-Speech với ClickSend API

[Các sếp đang gặp khó khăn khi phải gọi điện thoại thủ công cho hàng trăm khách hàng mỗi ngày? Workflow này sẽ giúp các sếp tự động hóa cuộc gọi thoại bằng Text-to-Speech (TTS) với ClickSend API, tiết kiệm thời gian và tăng hiệu quả giao tiếp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian gọi điện thủ công hàng giờ mỗi ngày.
- Tăng hiệu quả giao tiếp với khách hàng thông qua cuộc gọi thoại tự động.
- Tăng tính cá nhân hóa với nhiều giọng nói khác nhau.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ClickSend và API Key (đăng ký [tại đây](https://clicksend.com/?u=586989) và nhận 2€ miễn phí).
- Số điện thoại nhận cuộc gọi thoại.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Click vào menu "Workflow" > "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/3072`.
4. Click "Import".

Hoặc các sếp có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "options": {
          "method": "POST",
          "body": "{\n\t\"messages\": [\n\t\t{\n\t\t\t\"source\": \"php\",\n\t\t\t\"body\": \"{{$node[\"On form submission\"].json[\"data\"][\"text\"]}}\",\n\t\t\t\"to\": \"{{$node[\"On form submission\"].json[\"data\"][\"phone\"]}}\",\n\t\t\t\"country\": \"{{$node[\"On form submission\"].json[\"data\"][\"country\"]}}\",\n\t\t\t\"voice\": \"{{$node[\"On form submission\"].json[\"data\"][\"voice\"]}}\"\n\t\t}\n\t]\n}",
          "sendQuery": true,
          "sendHeaders": true,
          "sendBody": true,
          "url": "https://rest.clicksend.com/v3/voice/send"
        },
        "authentication": "predefinedCredentialType",
        "node": "n8n-nodes-base.httpRequest"
      },
      "name": "Send Voice",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        1000,
        400
      ]
    },
    {
      "parameters": {
        "options": {
          "schema": {
            "type": "object",
            "properties": {
              "text": {
                "type": "string",
                "title": "Text to speak",
                "description": "The text that will be spoken in the call"
              },
              "phone": {
                "type": "string",
                "title": "Phone number",
                "description": "The phone number that will receive the call"
              },
              "country": {
                "type": "string",
                "title": "Country code",
                "description": "The country code of the phone number (e.g. US, GB, IT)"
              },
              "voice": {
                "type": "string",
                "title": "Voice",
                "description": "The voice that will be used to speak the text",
                "enum": [
                  "male",
                  "female"
                ]
              }
            },
            "required": [
              "text",
              "phone",
              "country",
              "voice"
            ]
          }
        },
        "node": "n8n-nodes-base.formTrigger"
      },
      "name": "On form submission",
      "type": "n8n-nodes-base.formTrigger",
      "typeVersion": 1,
      "position": [
        600,
        400
      ]
    }
  ],
  "connections": [
    {
      "node": "On form submission",
      "type": "main",
      "index": 0,
      "target": "Send Voice"
    }
  ],
  "settings": {
    "saveManualExecutions": true,
    "saveExecutionProgress": true,
    "saveDataErrorExecution": "all",
    "saveDataSuccessExecution": "all",
    "executionTimeout": 3600,
    "timezone": ""
  },
  "createdAt": "2023-08-15T12:00:00.000Z",
  "updatedAt": "2023-08-15T12:00:00.000Z"
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Send Voice"**:
   - Tạo một "Basic Auth" credential với:
     - Username: Email đăng ký ClickSend
     - Password: API Key từ ClickSend
   - Đảm bảo đã chọn đúng credential này trong node "Send Voice".

2. **Node "On form submission"**:
   - Cấu hình form với các trường bắt buộc:
     - Text to speak: Nội dung muốn chuyển thành giọng nói
     - Phone number: Số điện thoại nhận cuộc gọi
     - Country code: Mã quốc gia của số điện thoại (ví dụ: US, GB, IT)
     - Voice: Chọn giọng nam hoặc nữ

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách submit form với các thông tin thử nghiệm.
2. Kiểm tra số điện thoại đã nhập để nghe cuộc gọi thoại tự động.
3. Bật Active workflow để kích hoạt chế độ tự động hóa hoàn chỉnh.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi cuộc gọi thoại được gửi thành công.
- Lưu log cuộc gọi thoại vào Google Sheets để theo dõi lịch sử giao tiếp.
- Tạo nhiều workflow khác nhau với các giọng nói và nội dung khác nhau cho các trường hợp sử dụng khác nhau.

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa cuộc gọi thoại hoàn hảo cho các doanh nghiệp cần giao tiếp thoại hiệu quả. Với ClickSend API và n8n, các sếp có thể tiết kiệm thời gian và tăng hiệu quả giao tiếp một cách đáng kể. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa cuộc gọi thoại!