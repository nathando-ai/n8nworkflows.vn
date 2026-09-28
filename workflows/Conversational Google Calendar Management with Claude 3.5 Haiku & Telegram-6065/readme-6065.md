---
title: "🚀 Quản lý Lịch Google bằng Claude 3.5 Haiku & Telegram – Tự động 100% không code"
description: "Tự động tạo, xem và chỉnh sửa sự kiện Google Calendar ngay trong chat Telegram nhờ AI Claude 3.5 Haiku, giảm 90% công việc thủ công."
slug: "quan-ly-lich-google-telegram-claude"
tags: [n8n, automation, no-code, personal-productivity, ai-chatbot, google-calendar, telegram]
keywords: [n8n workflow, tự động hóa, Google Calendar, Telegram bot, Claude AI, AI chatbot]
---

# 🚀 Quản lý Lịch Google bằng Claude 3.5 Haiku & Telegram

Bạn có bao giờ phải mở Google Calendar, sao chép ngày giờ, rồi quay lại Telegram để thông báo cho đồng nghiệp?  
Việc **đánh máy thủ công**, **đối chiếu thời gian** và **sửa lỗi nhập liệu** khiến năng suất giảm mạnh, đặc biệt với những người làm việc từ xa hoặc quản lý nhiều dự án.

**Workflow này** sẽ biến Telegram thành trợ lý ảo thông minh:  
- Nhận lệnh từ người dùng (tạo, xem, xóa sự kiện).  
- AI Claude 3.5 Haiku phân tích ngôn ngữ tự nhiên, tạo prompt cho Google Calendar.  
- Kết quả được trả về ngay trong cùng một cuộc trò chuyện Telegram.  

> **Bạn sẽ có một công cụ “Chat‑to‑Calendar” hoàn toàn không cần viết một dòng code nào.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo/kiểm tra sự kiện chỉ trong vài giây qua tin nhắn.  
- **Độ chính xác cao**: AI chuyển ngôn ngữ tự nhiên thành định dạng chuẩn của Google Calendar.  
- **Hoạt động liên tục**: Bot luôn sẵn sàng 24/7, không cần mở giao diện web.  
- **Tùy biến dễ dàng**: Thêm các lệnh mới (nhắc nhở, báo cáo) chỉ bằng một node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Thành phần | Mô tả | Ghi chú |
|------------|------|---------|
| **Telegram Bot API** | Token bot và Chat ID | Tạo bot qua BotFather |
| **Google Calendar OAuth2** | Credential cho Google Calendar | Cấp quyền `https://www.googleapis.com/auth/calendar` |
| **Anthropic API** | API key cho Claude 3.5 Haiku | Đăng ký tại https://www.anthropic.com |
| **OpenAI API** (tùy chọn) | API key cho mô hình GPT‑4.1‑mini (fallback) | Dùng khi Claude không đáp ứng |
| **n8n** | Phiên bản ≥ 1.0, chạy trên VPS hoặc Docker | Đảm bảo các node đã được cài |
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Chọn **Workflows → Import**.  
3. Tải file JSON của workflow (được cung cấp ở cuối README) hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard**.  
4. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần thay đổi | Hướng dẫn chi tiết |
|------|----------------------|--------------------|
| **Telegram Trigger** | **Credentials → telegramApi** → nhập Token Bot | Đặt **Chat ID** (nếu muốn giới hạn bot chỉ trả lời trong một nhóm/chát). |
| **AI Agent** | **Prompt** (trong phần “Base + Fallback”) | Đặt prompt mô tả cách hiểu lệnh người dùng (ví dụ: “Bạn là trợ lý lịch, hãy phân tích câu lệnh và trả về JSON gồm `action`, `title`, `start`, `end`, `description`”). |
| **4.1‑nano** (lmChatOpenAi) | **Credentials → openAiApi** → API Key | Chọn model **gpt‑4.1‑mini** (được preset). |
| **Create** (googleCalendarTool) | **Operation → create** | Định dạng dữ liệu đầu vào: `summary`, `start.dateTime`, `end.dateTime`, `description`. Sử dụng output của **AI Agent** hoặc **Haiku 3.5**. |
| **Get** (googleCalendarTool) | **Operation → getAll** | Thiết lập **Time Min** và **Time Max** (có thể lấy từ message hoặc mặc định 30 ngày tới). |
| **Explain** (telegramTool) | **Operation → sendAndWait** | Dùng để hỏi AI bổ sung thông tin nếu lệnh chưa đủ chi tiết. |
| **Haiku 3.5** (lmChatAnthropic) | **Credentials → anthropicApi** → API Key | Model **claude-3-5-haiku-20241022** đã được preset. |
| **Result** (telegram) | **Credentials → telegramApi** → Token Bot | Nội dung tin nhắn trả về: sử dụng output của **Create/Get** hoặc **Explain**. |

> **Lưu ý:** Đảm bảo **Credentials** được gán cho mỗi node, nếu không workflow sẽ báo lỗi “Missing credentials”.

#### 3. Kích hoạt ⚡️
1. Nhấn **Save** → **Activate**.  
2. Mở Telegram, gửi lệnh tới bot (ví dụ: “Tạo cuộc họp dự án ngày 15/10 14h – 15h”).  
3. Kiểm tra phản hồi: bot sẽ trả kết quả tạo sự kiện hoặc danh sách sự kiện trong khoảng thời gian yêu cầu.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack**: Thêm node `slackTool` để đồng thời gửi thông báo lên kênh Slack.  
- **Lưu log**: Dùng node `Google Sheets` hoặc `Postgres` để ghi lại mọi lệnh và kết quả, hỗ trợ audit.  
- **Báo cáo định kỳ**: Thêm `Cron` node chạy mỗi tuần, lấy danh sách sự kiện và gửi báo cáo PDF qua email.  
- **Nhắc nhở tự động**: Sử dụng `Google Calendar Tool → getAll` + `Telegram Tool → send` để gửi reminder 15 phút trước mỗi sự kiện.  

### 📌 Kết luận
Với workflow **Conversational Google Calendar Management with Claude 3.5 Haiku & Telegram**, các sếp có thể biến Telegram thành trợ lý lịch thông minh, giảm thiểu công việc nhập liệu và tăng độ chính xác. Hãy **import ngay**, cấu hình các credentials, và để bot làm việc cho bạn 24/7!  

---  

## 📦 File JSON Workflow (copy vào “Import from Clipboard”)

```json
{
  "nodes": [
    {
      "name": "Telegram Trigger",
      "type": "telegramTrigger",
      "credentials": ["telegramApi"]
    },
    {
      "name": "AI Agent",
      "type": "agent"
    },
    {
      "name": "4.1-nano",
      "type": "lmChatOpenAi",
      "credentials": ["openAiApi"],
      "keyParameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "gpt-4.1-mini",
          "cachedResultName": "gpt-4.1-mini"
        }
      }
    },
    {
      "name": "Create",
      "type": "googleCalendarTool",
      "credentials": ["googleCalendarOAuth2Api"]
    },
    {
      "name": "Get",
      "type": "googleCalendarTool",
      "credentials": ["googleCalendarOAuth2Api"],
      "keyParameters": {
        "operation": "getAll"
      }
    },
    {
      "name": "Explain",
      "type": "telegramTool",
      "credentials": ["telegramApi"],
      "keyParameters": {
        "operation": "sendAndWait"
      }
    },
    {
      "name": "Haiku 3.5",
      "type": "lmChatAnthropic",
      "credentials": ["anthropicApi"],
      "keyParameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "claude-3-5-haiku-20241022",
          "cachedResultName": "Claude Haiku 3.5"
        }
      }
    },
    {
      "name": "Result",
      "type": "telegram",
      "credentials": ["telegramApi"]
    }
  ],
  "connections": {
    "Telegram Trigger": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
      "main": [
        [
          {
            "node": "4.1-nano",
            "type": "main",
            "index": 0
          },
          {
            "node": "Haiku 3.5",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "4.1-nano": {
      "main": [
        [
          {
            "node": "Create",
            "type": "main",
            "index": 0
          },
          {
            "node": "Get",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Haiku 3.5": {
      "main": [
        [
          {
            "node": "Explain",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Create": {
      "main": [
        [
          {
            "node": "Result",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get": {
      "main": [
        [
          {
            "node": "Result",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Explain": {
      "main": [
        [
          {
            "node": "Result",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {}
}
```

---  

**Áp dụng ngay** để biến Telegram thành trợ lý lịch AI, nâng cao năng suất cá nhân và đội nhóm! 🚀