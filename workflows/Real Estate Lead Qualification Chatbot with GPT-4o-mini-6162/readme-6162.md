---
title: "🤖 Chatbot Chuyển Giao Lead Tài Sản Bất Động Sản Với GPT-4o-mini - Tự Động Hóa 100% Không Code"
description: "Tự động hóa quá trình phỏng vấn và lọc lead chất lượng cho doanh nghiệp bất động sản bằng chatbot AI sử dụng GPT-4o-mini, tiết kiệm thời gian và tăng tỷ lệ chuyển đổi lên đến 40%."
slug: "chatbot-qualification-lead-real-estate-gpt4o-mini"
tags: [n8n, automation, no-code, ai-chatbot, real-estate, lead-nurturing]
keywords: [n8n workflow bất động sản, chatbot AI lead qualification, tự động hóa phỏng vấn lead, GPT-4o-mini n8n, tự động hóa bất động sản]
---

# 🚀 Chatbot Chuyển Giao Lead Tài Sản Bất Động Sản Với GPT-4o-mini

### **Giải pháp AI tự động hóa phỏng vấn và lọc lead chất lượng cho doanh nghiệp bất động sản**
Hiện nay, các sếp bất động sản thường phải tốn thời gian quý báu để:
- Phỏng vấn hàng trăm lead mỗi ngày qua email, zalo hoặc website
- Lọc ra những lead thực sự có nhu cầu và khả năng mua
- Ghi nhớ thông tin khách hàng trong nhiều cuộc trò chuyện
- Theo dõi tiến trình của từng lead một cách thủ công

**Workflow này giải quyết tất cả những vấn đề trên bằng một chatbot AI thông minh**, sử dụng GPT-4o-mini để:
✅ **Phỏng vấn tự động** khách hàng qua website hoặc webhook
✅ **Lọc lead chất lượng** dựa trên tiêu chí doanh nghiệp đặt ra
✅ **Ghi nhớ lịch sử cuộc trò chuyện** để tiếp tục từ điểm dừng
✅ **Tích hợp hoàn toàn** với hệ thống CRM hoặc email của bạn

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 với hiệu suất tối ưu, các sếp nên cài đặt n8n trên VPS riêng (Self-hosted) để đảm bảo:
- Tính bảo mật cao (không phụ thuộc vào cloud công cộng)
- Tốc độ phản hồi nhanh chóng
- Hoạt động liên tục không bị giới hạn API

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/ngày** cho đội ngũ chăm sóc khách hàng
- **Tăng tỷ lệ chuyển đổi lead** lên đến 40% nhờ AI lọc lead chất lượng
- **Tự động ghi nhớ lịch sử** cuộc trò chuyện với khách hàng
- **Hoạt động 24/7** mà không cần nhân viên trực ca
- **Tích hợp dễ dàng** với hệ thống CRM hoặc email hiện có
- **Cải thiện trải nghiệm khách hàng** với phản hồi tức thời
:::

---

## 🔧 Yêu cầu cần thiết

Trước khi triển khai workflow, các sếp cần chuẩn bị:

1. **Tài khoản OpenAI** với API Key (để sử dụng GPT-4o-mini)
   - [Đăng ký tài khoản OpenAI](https://platform.openai.com/signup)
   - Mua gói API phù hợp với nhu cầu (từ $0.000005/1000 token)

2. **Domain hoặc URL** để tạo webhook
   - Ví dụ: `https://tendomain.com/chatbot-webhook`

3. **N8n Self-hosted** (không dùng phiên bản cloud)
   - Cài đặt theo hướng dẫn: [n8n.io/docs/self-hosted](https://n8n.io/docs/self-hosted)

4. **(Tùy chọn)** Tài khoản CRM hoặc email như:
   - Google Sheets
   - Airtable
   - Mailchimp
   - CRM nội bộ

---

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

**Bước 1:** Tải workflow từ [n8n.io/workflows/6162](https://n8n.io/workflows/6162) hoặc copy JSON dưới đây:

```json
{
  "nodes": [
    {
      "parameters": {
        "path": "chatbot-webhook",
        "httpMethod": "POST",
        "responseType": "text"
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {},
      "name": "Set User Message",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [450, 300]
    },
    {
      "parameters": {
        "agentType": "langchain",
        "model": "gpt-4o-mini",
        "tools": [],
        "memory": "Simple Memory"
      },
      "name": "AI Agent",
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1,
      "position": [650, 300]
    },
    {
      "parameters": {},
      "name": "Respond to Webhook",
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1,
      "position": [850, 300]
    },
    {
      "parameters": {
        "model": {
          "mode": "list",
          "value": "gpt-4o-mini"
        }
      },
      "name": "OpenAI Chat Model",
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1,
      "position": [650, 150]
    },
    {
      "parameters": {
        "windowSize": 3,
        "memoryKey": "chat_history"
      },
      "name": "Simple Memory",
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1,
      "position": [650, 450]
    }
  ],
  "connections": {
    "Webhook": {
      "main": [
        [
          {
            "node": "Set User Message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Set User Message": {
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
            "node": "Respond to Webhook",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "model",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "memory",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

**Bước 2:** Trong n8n Editor:
1. Nhấp vào **Import** (icon file)
2. Chọn **Paste JSON** và dán nội dung JSON trên
3. Nhấp **Import**

---

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

#### **A. Cấu hình Webhook**
1. Trong node **Webhook**:
   - Đảm bảo **path** là `chatbot-webhook` (không đổi)
   - **HTTP Method** phải là `POST`
   - **Response Type** chọn `text`

#### **B. Cấu hình OpenAI API**
1. Trong node **OpenAI Chat Model**:
   - Chọn **model** là `gpt-4o-mini`
   - Nhấp vào **Credentials** và chọn tài khoản OpenAI đã tạo
   - Điền **API Key** từ tài khoản OpenAI

#### **C. Cấu hình AI Agent**
1. Trong node **AI Agent**:
   - **Agent Type** giữ nguyên `langchain`
   - **Model** tự động lấy từ node OpenAI Chat Model
   - **Memory** chọn `Simple Memory` (đã kết nối)

#### **D. Cấu hình Simple Memory**
1. Trong node **Simple Memory**:
   - **Window Size** (số cuộc trò chuyện lưu): 3 (có thể tăng lên 5-10)
   - **Memory Key** giữ nguyên `chat_history`

#### **E. Cấu hình Set User Message**
1. Trong node **Set User Message**:
   - Thêm một **Expression** để định dạng dữ liệu đầu vào:
     ```json
     {
       "userMessage": "$json.userMessage",
       "chat_history": "$json.chat_history || []"
     }
     ```
   - Nếu muốn thêm logic lọc lead, có thể thêm vào node này:
     ```json
     {
       "userMessage": "$json.userMessage",
       "isQualified": "$json.userMessage.includes('muốn mua nhà') || $json.userMessage.includes('nghĩ về mua đất')"
     }
     ```

#### **F. Cấu hình Respond to Webhook**
1. Trong node **Respond to Webhook**:
   - **Response Type** chọn `text`
   - **Response** có thể là:
     ```json
     {
       "responseType": "text",
       "response": "$node["AI Agent"].json.output.main[0].response"
     }
     ```

---

### 3. Kích hoạt ⚡️

**Bước 1: Test Run**
1. Nhấp vào **Execute Node** trên node **Webhook**
2. Gửi một request POST đến URL webhook với payload:
   ```json
   {
     "userMessage": "Tôi đang tìm nhà ở quận 7, giá từ 1 tỷ"
   }
   ```
3. Kiểm tra kết quả phản hồi từ AI

**Bước 2: Active Workflow**
1. Nhấp vào **Active** trên thanh công cụ
2. Workflow sẽ bắt đầu hoạt động 24/7

---

## ✍️ Mẹo & gợi ý nâng cao

### **1. Tích hợp với Slack/Telegram để nhận báo cáo**
- Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi có lead mới:
  ```json
  {
    "message": "🚨 Lead mới: {{ $node["Set User Message"].json.output.main[0].userMessage }}"
  }
  ```

### **2. Lưu lead vào Google Sheets/Airtable**
- Thêm node **Google Sheets** sau node **Set User Message** để ghi dữ liệu:
  ```json
  {
    "sheetName": "Leads",
    "row": {
      "Tên": "$json.name",
      "Số điện thoại": "$json.phone",
      "Lời nhắn": "$json.userMessage",
      "Trạng thái": "$json.isQualified ? 'Chất lượng' : 'Không chất lượng'"
    }
  }
  ```

### **3. Tự động gửi email xác nhận**
- Sử dụng node **Email** để gửi email tự động sau khi phỏng vấn:
  ```json
  {
    "to": "$json.email",
    "subject": "Xác nhận thông tin mua nhà",
    "text": "Cảm ơn bạn đã liên hệ! Chúng tôi sẽ liên hệ lại trong 24h."
  }
  ```

### **4. Cập nhật hệ thống CRM**
- Tích hợp với **HubSpot**, **Zoho CRM** hoặc **Salesforce** để cập nhật lead mới:
  ```json
  {
    "properties": {
      "name": "$json.name",
      "email": "$json.email",
      "phone": "$json.phone",
      "lead_score": "$json.isQualified ? 100 : 50"
    }
  }
  ```

### **5. Tăng cường logic lọc lead**
- Thêm node **Function** để tự động phân loại lead:
  ```javascript
  // Nếu lead có từ khóa "muốn mua" hoặc "nghĩ về mua"
  if (userMessage.includes('muốn mua') || userMessage.includes('nghĩ về mua')) {
    return { isQualified: true, priority: 'cao' };
  } else {
    return { isQualified: false, priority: 'thấp' };
  }
  ```

---

## 📌 Kết luận

Workflow **Chatbot Chuyển Giao Lead Tài Sản Bất Động Sản Với GPT-4o-mini** là giải pháp **tự động hóa hoàn toàn** quá trình phỏng vấn và lọc lead cho doanh nghiệp bất động sản, giúp:
✔ **Tiết kiệm thời gian** cho đội ngũ chăm sóc khách hàng
✔ **Tăng tỷ lệ chuyển đổi** nhờ AI lọc lead chất lượng
✔ **Hoạt động 24/7** mà không cần nhân viên trực ca
✔ **Tích hợp dễ dàng** với hệ thống CRM hoặc email hiện có

**Hành động ngay!**
1. Cài đặt n8n trên VPS theo hướng dẫn
2. Import workflow và cấu hình API OpenAI
3. Test và active workflow
4. Tích hợp với hệ thống CRM của bạn

**🚀 Khám phá thêm:**
- [Tutorial cài đặt n8n Self-hosted](https://n8n.io/docs/self-hosted)
- [Hướng dẫn sử dụng GPT-4o-mini](https://platform.openai.com/docs/models/gpt-4o-mini)
- [Tích hợp n8n với Google Sheets](https://n8n.io/docs/integration/google-sheets)

---