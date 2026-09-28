---
title: "🤖 Tự Động Gọi Điện Xác Thực Lead B2B Với AI Voice Agent (VAPI + n8n)"
description: "Giải pháp tự động hóa quy trình gọi điện xác thực thông tin khách hàng tiềm năng (B2B) bằng AI Voice. Kết nối liền mạch từ Google Sheets đến VAPI, tiết kiệm 100% thời gian gọi thủ công."
slug: "tu-dong-goi-dien-xac-thuc-lead-b2b-vapi-n8n"
tags: [n8n, automation, ai-voice, vapi, lead-generation, b2b]
keywords: [n8n workflow, tự động hóa gọi điện, AI voice agent, VAPI integration, xác thực lead B2B]
---

# 🤖 Tự Động Gọi Điện Xác Thực Lead B2B Với AI Voice Agent (VAPI + n8n)

Trong môi trường kinh doanh B2B, việc thu thập lead từ các nguồn như form đăng ký, sự kiện hay quảng cáo thường chỉ mới dừng lại ở việc có được tên và số điện thoại. Tuy nhiên, dữ liệu thô này thường thiếu chính xác hoặc chưa đủ thông tin để đội sales tiếp cận hiệu quả. Việc gọi điện thủ công để xác thực thông tin (Xác nhận công ty, vị trí, thách thức đang gặp phải) là một quy trình tốn kém thời gian, dễ gây sai sót và khiến đội ngũ sales bị quá tải.

Workflow **B2B Lead Qualification** này là giải pháp "chốt hạ" cho vấn đề đó. Thay vì con người phải cầm máy gọi từng số, hệ thống sẽ tự động kích hoạt một **AI Voice Agent (thông qua VAPI)** để thực hiện cuộc gọi xác thực. AI sẽ trò chuyện tự nhiên, thu thập các thông tin quan trọng như tên, công ty và thách thức kinh doanh, sau đó lưu lại vào Google Sheets để đội sales chỉ việc "ăn sẵn" lead đã được sàng lọc kỹ càng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý các cuộc gọi voice thực tế, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian gọi điện:** AI thực hiện cuộc gọi 24/7, không cần nghỉ ngơi, không bị gián đoạn.
- **Dữ liệu Lead chất lượng cao:** Chỉ những lead đã được AI xác nhận thông tin (tên, công ty, vấn đề) mới được lưu vào CRM, giúp đội sales tập trung vào các khách hàng thực sự tiềm năng.
- **Trải nghiệm khách hàng nhất quán:** AI Voice Agent có giọng nói tự nhiên, xử lý tình huống linh hoạt, tạo ấn tượng chuyên nghiệp ngay từ lần tiếp xúc đầu tiên.
- **Tích hợp liền mạch:** Dữ liệu được đồng bộ tự động từ Google Sheets (nguồn lead) đến VAPI (gọi điện) và quay lại Google Sheets (kết quả), đóng vòng lặp hoàn chỉnh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1.  **Tài khoản n8n:** Bản self-hosted hoặc cloud.
2.  **Tài khoản Google:** Để tạo Google Sheets chứa danh sách lead và lưu kết quả.
3.  **Tài khoản VAPI.ai:** Nền tảng AI Voice Agent. Cần có API Key và ID của Agent đã cấu hình sẵn (Agent cần được thiết lập để gọi ra và gửi webhook về n8n).
4.  **Google Sheets:**
    -   Sheet 1: Chứa danh sách lead cần gọi (cột: Tên, Số điện thoại, v.v.).
    -   Sheet 2: Chứa kết quả cuộc gọi (cột: Tên, Công ty, Thách thức, Trạng thái, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON workflow từ link gốc [n8n.io/workflows/5404](https://n8n.io/workflows/5404) hoặc copy toàn bộ code JSON bên dưới và dán vào n8n Editor.

```json
{
  "name": "B2B lead qualification",
  "nodes": [
    {
      "parameters": {
        "operation": "rowAdded",
        "documentId": {
          "__rl": true,
          "value": "YOUR_GOOGLE_SHEET_ID",
          "mode": "id"
        },
        "sheetName": {
          "__rl": true,
          "value": "YOUR_SHEET_NAME",
          "mode": "name"
        },
        "pollTime": 30
      },
      "id": "unique-id-1",
      "name": "New Lead Captured",
      "type": "n8n-nodes-base.googleSheetsTrigger",
      "typeVersion": 1,
      "position": [0, 0],
      "credentials": {
        "googleSheetsTriggerOAuth2Api": {
          "id": "YOUR_CREDENTIAL_ID",
          "name": "Google Sheets Trigger"
        }
      }
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://api.vapi.ai/v1/call",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Authorization",
              "value": "Bearer YOUR_VAPI_API_KEY"
            }
          ]
        },
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "={{ JSON.stringify({\n  assistantId: 'YOUR_VAPI_ASSISTANT_ID',\n  phone: {{ $json['Phone Number'] }},\n  webhookUrl: 'YOUR_N8N_WEBHOOK_URL'\n}) }}",
        "options": {}
      },
      "id": "unique-id-2",
      "name": "Initiate Voice Call (VAPI)",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [220, 0]
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "documentId": {
          "__rl": true,
          "value": "YOUR_GOOGLE_SHEET_ID",
          "mode": "id"
        },
        "sheetName": {
          "__rl": true,
          "value": "YOUR_RESULT_SHEET_NAME",
          "mode": "name"
        },
        "columns": {
          "mappingMode": "autoMapInputData",
          "value": {
            "Name": "={{ $json.name }}",
            "Company": "={{ $json.company }}",
            "Challenges": "={{ $json.challenges }}",
            "Status": "Qualified"
          }
        },
        "options": {}
      },
      "id": "unique-id-3",
      "name": "Save Qualified Lead to CRM Sheet",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [440, 0],
      "credentials": {
        "googleApi": {
          "id": "YOUR_CREDENTIAL_ID",
          "name": "Google Sheets"
        }
      }
    },
    {
      "parameters": {
        "respondWith": "text",
        "responseBody": "Success"
      },
      "id": "unique-id-4",
      "name": "Send Call Data Acknowledgement",
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1.1,
      "position": [660, 0]
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "60d5fdeb-b5d8-4e71-90d0-182acc695404",
        "responseMode": "responseNode",
        "options": {}
      },
      "id": "unique-id-5",
      "name": "Receive Lead Details from VAPI",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1.1,
      "position": [220, 220]
    }
  ],
  "connections": {
    "New Lead Captured": {
      "main": [
        [
          {
            "node": "Initiate Voice Call (VAPI)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Receive Lead Details from VAPI": {
      "main": [
        [
          {
            "node": "Save Qualified Lead to CRM Sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Save Qualified Lead to CRM Sheet": {
      "main": [
        [
          {
            "node": "Send Call Data Acknowledgement",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

:::note[Lưu ý quan trọng]
Workflow trên có 2 luồng chính:
1. **Luồng kích hoạt:** `New Lead Captured` (Google Sheets) -> `Initiate Voice Call (VAPI)`.
2. **Luồng nhận kết quả:** `Receive Lead Details from VAPI` (Webhook) -> `Save Qualified Lead to CRM Sheet` -> `Send Call Data Acknowledgement`.
:::

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình chi tiết từng node sau:

**1. Node: `New Lead Captured` (Google Sheets Trigger)**
*   **Credentials:** Chọn credential Google Sheets đã kết nối.
*   **Document ID:** Chọn Sheet chứa danh sách lead cần gọi.
*   **Sheet Name:** Chọn tab cụ thể trong Sheet.
*   **Poll Time:** Mặc định 30s. Có thể giảm xuống 10s nếu cần tốc độ cao hơn (nhưng tốn quota API).
*   **Logic:** Workflow sẽ chạy mỗi khi có một hàng mới được thêm vào Sheet này. Đảm bảo Sheet có cột chứa **Số điện thoại** (ví dụ: `Phone Number`) để node HTTP Request có thể đọc.

**2. Node: `Initiate Voice Call (VAPI)` (HTTP Request)**
*   **URL:** `https://api.vapi.ai/v1/call` (Mặc định, không cần đổi).
*   **Headers:**
    *   `Authorization`: `Bearer YOUR_VAPI_API_KEY`. Thay `YOUR_VAPI_API_KEY` bằng API Key thật của bạn từ trang VAPI Dashboard.
*   **Body (JSON):**
    *   `assistantId`: Thay bằng ID của AI Agent (Assistant) mà bạn đã tạo trong VAPI. Agent này phải được thiết lập để **gọi ra (Outbound)** và có khả năng thu thập thông tin.
    *   `phone`: Dùng expression để lấy số điện thoại từ node trước: `={{ $json['Phone Number'] }}` (Đổi tên cột cho khớp với Sheet của bạn).
    *   `webhookUrl`: Đây là **điểm mấu chốt**. Các sếp cần lấy **Production URL** của node `Receive Lead Details from VAPI` (xem mục 4 bên dưới) và dán vào đây. Ví dụ: `https://your-n8n-domain.com/webhook/60d5fdeb-b5d8-4e71-90d0-182acc695404`.

**3. Node: `Receive Lead Details from VAPI` (Webhook)**
*   **Path:** Mặc định là `60d5fdeb-b5d8-4e71-90d0-182acc695404`. Các sếp có thể giữ nguyên hoặc đổi thành một chuỗi dễ nhớ hơn (ví dụ: `vapi-callback`). Nếu đổi, nhớ cập nhật lại URL trong node `Initiate Voice Call (VAPI)`.
*   **Response Mode:** Chọn `responseNode` (để node `Send Call Data Acknowledgement` xử lý phản hồi).
*   **Cấu hình trong VAPI:** Trong dashboard VAPI, khi thiết lập Assistant, các sếp cần cấu hình **Webhook** để gửi dữ liệu về địa chỉ này sau khi cuộc gọi kết thúc. Dữ liệu gửi về