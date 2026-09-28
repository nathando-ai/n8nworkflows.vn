---
title: "🍳 Tự động hóa gợi ý công thức từ nguyên liệu trong tủ lạnh với WhatsApp & AI Gemini"
description: "Hướng dẫn tự động hóa workflow n8n để nhận gợi ý công thức nấu ăn từ nguyên liệu trong tủ lạnh qua WhatsApp, sử dụng AI Gemini và API FatSecret."
slug: "tu-dong-hoa-goi-y-cong-thuc-tu-tu-lanh-voi-whatsapp-ai-gemini"
tags: [n8n, automation, no-code, WhatsApp, AI, FatSecret]
keywords: [n8n workflow, tự động hóa, AI Gemini, WhatsApp, FatSecret API]
---

# 🍳 Tự động hóa gợi ý công thức từ nguyên liệu trong tủ lạnh với WhatsApp & AI Gemini

[Các sếp] có bao giờ gặp tình trạng "tủ lạnh đầy nhưng không biết nấu gì" không? Với workflow này, các sếp có thể nhận ngay gợi ý công thức nấu ăn từ nguyên liệu trong tủ lạnh chỉ bằng một tin nhắn WhatsApp. Workflow kết hợp sức mạnh của AI Gemini và API FatSecret để mang đến những gợi ý thực tế và hữu ích.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tìm kiếm công thức trên mạng, chỉ cần gửi tin nhắn WhatsApp.
- **Gợi ý cá nhân hóa**: Nhận công thức phù hợp với nguyên liệu trong tủ lạnh của các sếp.
- **Hiệu quả nấu ăn**: Các sếp có thể nấu những món ăn ngon từ những nguyên liệu có sẵn.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow hoạt động liên tục 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (hoặc WhatsApp Business Solution).
- API Key từ Google Gemini.
- API Key từ FatSecret.
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào n8n Editor. Dưới đây là JSON của workflow:

```json
{
  "nodes": [
    {
      "name": "Simple Memory",
      "type": "memoryBufferWindow",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "name": "Google Gemini Chat Model1",
      "type": "lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        550,
        300
      ],
      "credentials": {
        "googlePalmApi": {
          "id": "your-google-palm-api-id"
        }
      }
    },
    {
      "name": "WhatsApp Trigger",
      "type": "whatsAppTrigger",
      "typeVersion": 1,
      "position": [
        50,
        300
      ],
      "credentials": {
        "whatsAppTriggerApi": {
          "id": "your-whatsapp-trigger-api-id"
        }
      }
    },
    {
      "name": "Send message",
      "type": "whatsApp",
      "typeVersion": 1,
      "position": [
        850,
        300
      ],
      "credentials": {
        "whatsAppApi": {
          "id": "your-whatsapp-api-id"
        }
      },
      "parameters": {
        "operation": "send"
      }
    },
    {
      "name": "Fatsecret_Recipes",
      "type": "httpRequestTool",
      "typeVersion": 1,
      "position": [
        350,
        300
      ],
      "credentials": {
        "oAuth2Api": {
          "id": "your-oauth2-api-id"
        }
      }
    },
    {
      "name": "The Chef Agent",
      "type": "agent",
      "typeVersion": 1,
      "position": [
        650,
        300
      ]
    }
  ],
  "connections": [
    {
      "node": "WhatsApp Trigger",
      "type": "main",
      "index": 0,
      "target": "Fatsecret_Recipes"
    },
    {
      "node": "Fatsecret_Recipes",
      "type": "main",
      "index": 0,
      "target": "The Chef Agent"
    },
    {
      "node": "The Chef Agent",
      "type": "main",
      "index": 0,
      "target": "Google Gemini Chat Model1"
    },
    {
      "node": "Google Gemini Chat Model1",
      "type": "main",
      "index": 0,
      "target": "Send message"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node WhatsApp Trigger**: Các sếp cần cấu hình credentials cho WhatsApp Trigger API.
- **Node Google Gemini Chat Model1**: Các sếp cần cấu hình credentials cho Google Palm API.
- **Node Send message**: Các sếp cần cấu hình credentials cho WhatsApp API.
- **Node Fatsecret_Recipes**: Các sếp cần cấu hình credentials cho OAuth2 API.

#### 3. Kích hoạt ⚡️
- Các sếp cần test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Sau khi test thành công, các sếp có thể bật Active workflow để sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận gợi ý công thức.
- Các sếp có thể lưu log các gợi ý công thức để tham khảo sau.
- Các sếp có thể gửi báo cáo định kỳ về các gợi ý công thức đã nhận.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nhận được gợi ý công thức nấu ăn từ nguyên liệu trong tủ lạnh. Các sếp chỉ cần gửi tin nhắn WhatsApp và nhận ngay gợi ý công thức từ AI Gemini và API FatSecret. Hãy áp dụng ngay workflow này để nâng cao hiệu quả nấu ăn của các sếp!