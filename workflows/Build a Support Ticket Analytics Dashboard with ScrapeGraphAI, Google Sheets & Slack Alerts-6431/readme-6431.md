---
title: "🚀 Tự Động Hóa Báo Cáo Analytics Ticket Hỗ Trợ với AI, Google Sheets & Thông Báo Slack (Không Cần Code)"
description: "Workflow tự động hóa phân tích ticket hỗ trợ 24/7 bằng AI ScrapeGraphAI, cập nhật dữ liệu vào Google Sheets và gửi báo cáo Slack tự động. Giúp các sếp theo dõi hiệu suất, phát hiện vi phạm SLA và cảnh báo kịp thời, tiết kiệm thời gian lên đến 15h/tuần."
slug: "tieu-dong-hoa-bao-cao-analytics-ticket-ai-google-sheets-slack"
tags: [n8n, automation, ticket-management, ai-summarization, google-sheets, slack-alerts, self-hosted]
keywords: [n8n workflow ticket hỗ trợ, tự động hóa phân tích ticket, AI ScrapeGraphAI, báo cáo Slack tự động, Google Sheets analytics, cảnh báo vi phạm SLA]
---

# 🚀 **Tự Động Hóa Báo Cáo Analytics Ticket Hỗ Trợ với AI, Google Sheets & Thông Báo Slack**

### **Giải pháp cho các sếp:**
Hãy tưởng tượng một ngày không phải lo lắng về việc **quên theo dõi ticket hỗ trợ**, **vi phạm SLA**, hoặc **phải tổng hợp báo cáo thủ công** vào cuối tuần. Workflow này sẽ **tự động hóa toàn bộ quy trình** bằng cách:
- **Scrape và phân tích** ticket từ hệ thống hỗ trợ (Zendesk, Freshdesk, ServiceNow...) bằng AI.
- **Cập nhật dữ liệu** vào **Google Sheets Dashboard** với các chỉ số KPI như thời gian phản hồi, tỷ lệ giải quyết, và xu hướng phổ biến.
- **Gửi cảnh báo Slack** khi có **vi phạm SLA** hoặc **ticket cấp cao** cần xử lý ưu tiên.
- **Tổng hợp báo cáo tự động** hàng ngày/tuần để các sếp **quản lý hiệu suất** một cách dễ dàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải tổng hợp báo cáo thủ công (giảm **15h/tuần**).
✅ **Phát hiện vi phạm SLA kịp thời**: Cảnh báo ngay khi ticket quá hạn.
✅ **Dữ liệu chính xác & tự động hóa**: Không lo sai sót do con người.
✅ **Quản lý hiệu suất dễ dàng**: Dashboard Google Sheets với **trend phân tích**, **tỷ lệ giải quyết**, và **tính năng AI phân loại ticket**.
✅ **Cảnh báo Slack ưu tiên**: Ticket cấp cao được gửi ngay đến Slack với **đánh giá rủi ro** từ AI.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ**               | **Thông tin cần thiết**                          | **Lưu ý**                                  |
|---------------------------|--------------------------------------------------|--------------------------------------------|
| **n8n (Self-hosted)**     | - VPS đã cài đặt n8n (n8n.io/docs/self-hosted)  | Sử dụng phiên bản **n8n Core** hoặc **n8n Enterprise** |
| **Google Sheets**         | - Email Google Workspace                          | Phải chia sẻ **Google Sheet** cho n8n (quyền **Chỉnh sửa**) |
| **Slack**                 | - Token API Slack (xApp)                         | Tạo tại: [Slack API](https://api.slack.com/apps) |
| **ScrapeGraphAI**         | - API Key (nếu sử dụng phiên bản trả phí)        | Nếu dùng **miễn phí**, có giới hạn scrape |
| **Hệ thống Ticket**       | - Webhook URL (nếu tích hợp Zendesk/Freshdesk)   | Cần cấu hình **Webhook Trigger** trong hệ thống |

### **2. Google Sheet mẫu**
Tạo một **Google Sheet** với cấu trúc sau (các sếp có thể sao chép từ [mẫu này](https://docs.google.com/spreadsheets/d/1XYZ...)):
| **Cột**                     | **Mô tả**                                  |
|-----------------------------|--------------------------------------------|
| `TicketID`                  | ID ticket từ hệ thống hỗ trợ               |
| `Status`                    | `Open` / `Closed` / `Escalated`           |
| `Category`                  | Phân loại tự động (Tech, Billing, Account) |
| `Priority`                  | `Critical` / `High` / `Medium`             |
| `ResponseTime`              | Thời gian phản hồi (giây)                  |
| `ResolutionTime`            | Thời gian giải quyết (giây)                |
| `CustomerTier`              | `VIP` / `Standard` / `Basic`               |
| `SLAStatus`                 | `Met` / `Breached`                         |
| `AI_Summary`                | Tóm tắt tự động từ AI                     |
| `EscalationReason`          | Lý do cần cấp cao (nếu có)                |

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6431](https://n8n.io/workflows/6431) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trang chủ của n8n sau khi cài đặt).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → **Create new workflow** → **Import from JSON**.
2. Dán toàn bộ mã JSON từ [n8n.io/workflows/6431](https://n8n.io/workflows/6431) (chọn **Export as JSON**).
3. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **🔹 Node 1: Automated Support Monitor Trigger (ScheduleTrigger)**
- **Cấu hình:**
  - **Frequency**: Đặt thành **Every hour** (hoặc tùy chỉnh theo nhu cầu).
  - **Timezone**: Chọn **UTC** hoặc timezone phù hợp với doanh nghiệp.
- **Lưu ý:** Nếu workflow chạy chậm, có thể tăng **frequency** lên **Every 2 hours**.

#### **🔹 Node 2: Support Ticket Webhook Trigger (Webhook)**
- **Cấu hình:**
  - **Path**: Giả định là `/support-ticket-webhook` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Sử dụng **API Key** (nếu hệ thống yêu cầu).
- **Lưu ý:**
  - Nếu tích hợp với **Zendesk/Freshdesk**, cần **cấu hình Webhook** trong hệ thống hỗ trợ để gửi dữ liệu đến URL này.
  - **Test Webhook** bằng cách gửi request từ Postman:
    ```json
    POST https://<your-n8n-domain>/webhook/support-ticket-webhook
    Headers:
      Content-Type: application/json
    Body:
      {
        "ticketId": "12345",
        "status": "open",
        "category": "technical",
        "priority": "high",
        "customerTier": "vip"
      }
    ```

#### **🔹 Node 3-5: AI Scraper (ScrapeGraphAI)**
- **Cấu hình chung:**
  - **API Key**: Nhập **API Key** của ScrapeGraphAI (nếu dùng phiên bản trả phí).
  - **URL Sources**:
    - **Open Tickets**: `https://your-support-system.com/tickets?status=open`
    - **Closed Tickets**: `https://your-support-system.com/tickets?status=closed`
    - **Knowledge Base**: `https://your-support-system.com/knowledge-base`
  - **Query Parameters** (ví dụ):
    ```json
    {
      "selectors": [
        { "id": "ticket-id", "selector": ".ticket-id" },
        { "id": "status", "selector": ".ticket-status" },
        { "id": "category", "selector": ".ticket-category" }
      ]
    }
    ```
- **Lưu ý:**
  - Nếu **ScrapeGraphAI không scrape được**, kiểm tra **CORS** và **robots.txt** của trang mục tiêu.
  - Dùng **miễn phí** có giới hạn scrape, nên **optimize query** để tránh bị block.

#### **🔹 Node 6: Advanced Support Analytics (Code)**
- **Mã mặc định** đã phân tích:
  - **Phân loại ticket** theo AI.
  - **Đánh giá SLA** (so sánh với tiêu chuẩn của doanh nghiệp).
  - **Tính toán điểm ưu tiên** cho escalation.
- **Lưu ý:**
  - Nếu cần **cập nhật logic**, mở **Code Node** → Chỉnh sửa mã JavaScript.
  - Ví dụ: Thêm **điều kiện mới** cho escalation:
    ```javascript
    if (jsonData.priority === "critical" && jsonData.responseTime > 3600) {
      jsonData.escalationReason = "Vi phạm SLA + Ticket cấp cao";
    }
    ```

#### **🔹 Node 7: Google Sheets Support Analytics Dashboard (GoogleSheets)**
- **Cấu hình:**
  - **Spreadsheet ID**: Sao chép từ URL Google Sheet (ví dụ: `1XYZ...` từ `https://docs.google.com/spreadsheets/d/1XYZ...`).
  - **Sheet Name**: Đặt tên là **"SupportAnalytics"** (hoặc chỉnh theo cấu trúc sheet của các sếp).
  - **Operation**: `appendOrUpdate` (để cập nhật dữ liệu mới).
  - **Headers**: Chọn **Use first row as headers**.
- **Lưu ý:**
  - **Chia sẻ Google Sheet** cho n8n với quyền **Chỉnh sửa**.
  - Nếu sheet **trống**, n8n sẽ tự tạo **cột mới** theo dữ liệu đầu tiên.

#### **🔹 Node 8 & 10: Critical Escalation Filter & Analytics Summary Filter (If)**
- **Cấu hình:**
  - **Condition**:
    - **Escalation Filter**:
      ```json
      {
        "jsonPath": "$",
        "values": [
          {
            "operator": "==",
            "property": "priority",
            "value": {
              "equals": "critical"
            }
          },
          {
            "operator": "==",
            "property": "SLAStatus",
            "value": {
              "equals": "breached"
            }
          }
        ]
      }
      ```
    - **Analytics Summary Filter**:
      ```json
      {
        "jsonPath": "$",
        "values": [
          {
            "operator": "==",
            "property": "status",
            "value": {
              "equals": "closed"
            }
          }
        ]
      }
      ```
- **Lưu ý:**
  - **Test condition** bằng cách **run workflow** với dữ liệu mẫu.

#### **🔹 Node 9 & 11: Slack Alerts (Slack)**
- **Cấu hình:**
  - **Token**: Nhập **Token API Slack** (tạo tại [Slack API](https://api.slack.com/apps)).
  - **Channel**: Chọn **#support-alerts** (hoặc channel phù hợp).
  - **Message Format**:
    - **Escalation Alert**:
      ```markdown
      *🚨 CRITICAL TICKET ESCALATION*
      Ticket ID: {{ $node["Support Ticket Webhook Trigger"].json["ticketId"] }}
      Status: {{ $node["Support Ticket Webhook Trigger"].json["status"] }}
      Priority: {{ $node["Support Ticket Webhook Trigger"].json["priority"] }}
      Reason: {{ $node["Advanced Support Analytics"].json["escalationReason"] }}
      ```
    - **Analytics Summary**:
      ```markdown
      *📊 DAILY SUPPORT ANALYTICS REPORT*
      Closed Tickets: {{ $node["AI Closed Tickets Analyzer"].json.length }}
      Avg Resolution Time: {{ $node["Advanced Support Analytics"].json["avgResolutionTime"] }}s
      Top Category: {{ $node["AI Support Dashboard Scraper"].json["topCategory"] }}
      ```
- **Lưu ý:**
  - **Test Slack Alert** bằng cách **run workflow** với dữ liệu mẫu.
  - **Rich formatting** (emoji, code block) giúp báo cáo **đẹp mắt hơn**.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Sử dụng **Webhook Trigger** để gửi request mẫu (ví dụ từ Postman).
   - Kiểm tra **Google Sheets** và **Slack** có nhận dữ liệu không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Monitor logs** trong **n8n Dashboard** để đảm bảo không có lỗi.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với hệ thống ticket hiện có**
- **Zendesk/Freshdesk**: Cấu hình **Webhook** trong hệ thống để gửi dữ liệu tự động.
- **ServiceNow**: Sử dụng **REST API** để scrape ticket.

### **2. Cải thiện AI Analysis**
- **Training ScrapeGraphAI**: Nếu dữ liệu ticket có **cấu trúc đặc biệt**, có thể **train AI** để scrape chính xác hơn.
- **Custom Prompt**: Sử dụng **ScrapeGraphAI** với **prompt tùy chỉnh** để phân loại ticket:
  ```json
  {
    "prompt": "Phân loại ticket này vào danh mục nào: Tech, Billing, Account, hoặc Customer Support? Nếu là Tech, hãy chỉ ra lỗi cụ thể (ví dụ: 'App crash khi login')."
  }
  ```

### **3. Tự động hóa báo cáo định kỳ**
- **Schedule Trigger** có thể chạy **hàng ngày/tuần** để gửi **báo cáo tổng hợp** qua Slack/Email.
- **Gửi Email tự động** bằng **Node Email** (n8n-nodes-base.email).

### **4. Lưu log & Audit Trail**
- Sử dụng **Node StickyNote** để lưu **lịch sử ticket** và **lý do escalation**.
- **Export log** vào **Google Drive** bằng **Node Google Drive**.

### **5