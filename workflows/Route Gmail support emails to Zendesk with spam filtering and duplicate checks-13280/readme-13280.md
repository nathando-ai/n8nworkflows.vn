---
title: "🚀 Tự Động Hóa Email Hỗ Trợ Sang Zendesk: Lọc Spam & Tránh Trùng Lặp 100% Không Code"
description: "Giải pháp tự động hóa hoàn chỉnh chuyển đổi email hỗ trợ sang Zendesk với hệ thống lọc spam và kiểm tra trùng lặp tự động, tiết kiệm 80% thời gian cho bộ phận hỗ trợ. Đảm bảo không bỏ lỡ yêu cầu nào và duy trì hệ thống ticket sạch sẽ."
slug: "tieu-dong-hoa-email-zendesk-spam-trung-lap"
tags: [n8n, automation, ticket-management, gmail, zendesk, no-code, email-processing]
keywords: [n8n workflow Zendesk, tự động hóa email hỗ trợ, lọc spam email, tránh trùng lặp ticket, Zendesk automation, n8n gmail trigger]
---

# 🚀 **Tự Động Hóa Email Hỗ Trợ Sang Zendesk: Lọc Spam & Tránh Trùng Lặp 100% Không Code**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, bộ phận hỗ trợ của các sếp phải:
- **Lặp đi lặp lại** mở email, sao chép nội dung sang Zendesk, và phân loại ticket thủ công.
- **Bị tràn ngập spam**, lãng phí thời gian kiểm tra email không liên quan.
- **Lo ngại trùng lặp**, dẫn đến ticket bị tạo nhiều lần cho cùng một vấn đề.
- **Bỏ lỡ yêu cầu khách hàng** khi không theo dõi email kịp thời.

**Workflow này giải quyết tất cả!** Nó tự động chuyển đổi **tất cả email hỗ trợ** thành ticket Zendesk, **lọc bỏ spam**, và **tránh trùng lặp**, giúp bộ phận hỗ trợ tập trung vào việc giải quyết vấn đề thực sự.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** của bộ phận hỗ trợ (không cần sao chép email thủ công).
✅ **Lọc spam tự động**, giảm thiểu email không liên quan đến Zendesk.
✅ **Tránh trùng lặp ticket**, đảm bảo mỗi vấn đề chỉ được xử lý một lần.
✅ **Tự động phân loại ticket** bằng tags (ví dụ: "refund", "damaged", "billing").
✅ **Hoạt động 24/7**, không bỏ lỡ yêu cầu khách hàng nào.
✅ **Dữ liệu sạch sẽ**, Zendesk không bị tràn ngập ticket trùng lặp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để n8n đọc email hỗ trợ):
   - **OAuth 2.0 Credentials** (cài đặt trong n8n: `Settings > Credentials > Add Credential > Gmail OAuth2`).
   - **Inbox email hỗ trợ** (ví dụ: `support@domaintiengviet.com`).
2. **Tài khoản Zendesk**:
   - **OAuth 2.0 API Credentials** (cài đặt trong n8n: `Settings > Credentials > Add Credential > Zendesk OAuth2`).
   - **API Key** từ Zendesk (thường là `subdomain.zendesk.com`).
3. **Danh sách tags Zendesk** (nếu muốn tự động thêm tags như "refund", "damaged").
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/13280) hoặc copy/paste JSON từ đây:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "New Support Email Trigger",
        "type": "n8n-nodes-base.gmailTrigger",
        "credentials": {
          "gmailOAuth2": "gmailOAuth2"
        }
      },
      {
        "parameters": {
          "code": "return $input.all();"
        },
        "name": "Spam Detection & Filtering",
        "type": "n8n-nodes-base.code"
      },
      {
        "parameters": {
          "properties": [
            {
              "name": "customerName",
              "value": "=($json['payload']['from']['displayName'] || $json['payload']['from']['email'].split('@')[0])"
            },
            {
              "name": "customerEmail",
              "value": "=$json['payload']['from']['email']"
            },
            {
              "name": "subject",
              "value": "=$json['payload']['subject']"
            },
            {
              "name": "messageBody",
              "value": "=$json['payload']['data']"
            },
            {
              "name": "threadId",
              "value": "=$json['payload']['threadId']"
            }
          ]
        },
        "name": "Extract & Normalize Email Data",
        "type": "n8n-nodes-base.set"
      },
      {
        "parameters": {
          "code": "const tags = [];\nif ($input.all()[0].subject.toLowerCase().includes('refund')) {\n  tags.push('refund');\n}\nif ($input.all()[0].subject.toLowerCase().includes('damaged')) {\n  tags.push('damaged');\n}\nif ($input.all()[0].subject.toLowerCase().includes('billing')) {\n  tags.push('billing');\n}\n\nreturn {\n  ...$input.all()[0],\n  tags: tags\n};"
        },
        "name": "Auto-Tag Ticket Based on Email Content",
        "type": "n8n-nodes-base.code"
      },
      {
        "parameters": {
          "operation": "getAll",
          "url": "=($credentials.zendeskOAuth2.url + '/api/v2/tickets.json')",
          "authentication": "OAuth2",
          "credentials": {
            "oauth": "zendeskOAuth2Api"
          }
        },
        "name": "Zendesk – Fetch Existing Tickets",
        "type": "n8n-nodes-base.zendesk"
      },
      {
        "parameters": {
          "collectionMode": "collect"
        },
        "name": "Merge Email With Existing Tickets",
        "type": "n8n-nodes-base.merge"
      },
      {
        "parameters": {
          "code": "const emailData = $input.all()[0];\nconst existingTickets = $input.all()[1].json;\n\n// Normalize subject for comparison\nconst normalizedSubject = emailData.subject.toLowerCase().trim();\n\n// Check if any existing ticket has a similar subject\nconst isDuplicate = existingTickets.some(ticket => {\n  const ticketSubject = ticket.subject.toLowerCase().trim();\n  return ticketSubject === normalizedSubject ||\n         ticketSubject.includes(normalizedSubject) ||\n         normalizedSubject.includes(ticketSubject);\n});\n\nreturn {\n  isDuplicate: isDuplicate,\n  emailData: emailData\n};"
        },
        "name": "Detect Duplicate Ticket by Subject",
        "type": "n8n-nodes-base.code"
      },
      {
        "parameters": {
          "condition": {
            "expression": "=!$input.currentNode.metadata.isDuplicate"
          }
        },
        "name": "Is This a New Ticket?",
        "type": "n8n-nodes-base.if"
      },
      {
        "parameters": {
          "url": "=($credentials.zendeskOAuth2.url + '/api/v2/tickets.json')",
          "authentication": "OAuth2",
          "credentials": {
            "oauth": "zendeskOAuth2Api"
          },
          "requestMethod": "POST",
          "body": {
            "type": "json",
            "value": "={\n  \"ticket\": {\n    \"subject\": $input.currentNode.metadata.emailData.subject,\n    \"comment\": {\n      \"body\": $input.currentNode.metadata.emailData.messageBody\n    },\n    \"requester_id\": \"=($input.currentNode.metadata.emailData.customerEmail.split('@')[0] || 'unknown')\",\n    \"tags\": $input.currentNode.metadata.emailData.tags.join(', '),\n    \"custom_fields\": [\n      {\n        \"id\": \"=($customFieldIdForEmail || 'custom_field_id_here')\",\n        \"value\": $input.currentNode.metadata.emailData.customerEmail\n      }\n    ]\n  }\n}"
        },
        "name": "Create Zendesk Support Ticket",
        "type": "n8n-nodes-base.zendesk"
      }
    ],
    "connections": {
      "New Support Email Trigger": {
        "main": [
          [
            {
              "node": "Spam Detection & Filtering",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Spam Detection & Filtering": {
        "main": [
          [
            {
              "node": "Extract & Normalize Email Data",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Extract & Normalize Email Data": {
        "main": [
          [
            {
              "node": "Auto-Tag Ticket Based on Email Content",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Auto-Tag Ticket Based on Email Content": {
        "main": [
          [
            {
              "node": "Zendesk – Fetch Existing Tickets",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Zendesk – Fetch Existing Tickets": {
        "main": [
          [
            {
              "node": "Merge Email With Existing Tickets",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Merge Email With Existing Tickets": {
        "main": [
          [
            {
              "node": "Detect Duplicate Ticket by Subject",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Detect Duplicate Ticket by Subject": {
        "main": [
          [
            {
              "node": "Is This a New Ticket?",
              "type": "main",
              "index": 0
            }
          ]
        ],
        "ifTrue": [
          [
            {
              "node": "Create Zendesk Support Ticket",
              "type": "main",
              "index": 0
            }
          ]
        ]
      }
    }
  }
  ```
- **Import vào n8n Editor**:
  - Mở n8n Workflow Editor → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
  - Nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

| **Node**                          | **Cần Chỉnh Sửa Gì?**                                                                 | **Hướng Dẫn**                                                                 |
|-----------------------------------|--------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **New Support Email Trigger**     | Chọn **credentials** `gmailOAuth2` (đã cài đặt trước).                                | Kiểm tra lại trong `Settings > Credentials` để đảm bảo OAuth2 được cấu hình. |
| **Spam Detection & Filtering**    | **Không cần chỉnh** (sử dụng mã JavaScript mặc định).                             | Nếu muốn thay đổi logic lọc spam, mở node này và chỉnh `code`.                |
| **Extract & Normalize Email Data**| **Không cần chỉnh** (trích xuất tự động tên, email, chủ đề, nội dung).           | Nếu email có định dạng đặc biệt, chỉnh `properties` trong node `Set`.          |
| **Auto-Tag Ticket Based on Email Content** | **Chỉnh tags** nếu muốn thêm/loại bỏ tags tự động.                          | Ví dụ: Thêm `tags.push('urgent')` nếu chủ đề chứa "urgent".                   |
| **Zendesk – Fetch Existing Tickets** | **Không cần chỉnh** (sử dụng OAuth2 đã cài đặt).                                | Đảm bảo `zendeskOAuth2Api` trong `credentials` là chính xác.                   |
| **Detect Duplicate Ticket by Subject** | **Không cần chỉnh** (so sánh chủ đề tự động).                                | Nếu muốn thêm logic phức tạp, chỉnh `code` trong node.                         |
| **Create Zendesk Support Ticket** | **Chỉnh `customFieldIdForEmail`** (nếu Zendesk có trường tùy chỉnh).              | Tìm ID trường tùy chỉnh trong Zendesk (ví dụ: `custom_field_id_here`).         |

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi một email mẫu đến inbox hỗ trợ (ví dụ: `support@domaintiengviet.com`).
   - Vào n8n Workflow Editor → Chọn workflow → Nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra Zendesk xem ticket có được tạo không.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau node `Create Zendesk Support Ticket` để thông báo ticket mới.
   - **Cách làm**:
     ```json
     {
       "parameters": {
         "channel": "#support-alerts",
         "text": "New ticket created: {{$node["Create Zendesk Support Ticket"].json.subject}}",
         "credentials": {
           "slack": "slackOAuth2"
         }
       },
       "name": "Notify Slack",
       "type": "n8n-nodes-base.slack"
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm node `n8n-nodes-base.googleSheets` để ghi lại tất cả ticket mới vào một sheet Google Sheets.
   - **Cách làm**:
     ```json
     {
       "parameters": {
         "sheetName": "Support_Tickets_Log",
         "row": {
           "Ticket_Subject": "{{$node["Create Zendesk Support Ticket"].json.subject}}",
           "Customer_Email": "{{$node["Extract & Normalize Email Data"].json.customerEmail}}",
           "Created_