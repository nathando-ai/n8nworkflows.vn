---
title: "🤖 **Cổng Lối AI Thông Minh: Tự Động Hóa Gọi API Bằng Claude AI Và MCP Protocol**"
description: "Workflow này chuyển đổi API truyền thống thành công cụ AI truy cập được thông qua MCP (Model Context Protocol), cho phép Claude AI tương tác an toàn, chi tiết và có thể theo dõi với mọi hệ thống doanh nghiệp (CRM, ERP, Database, SaaS) qua một giao diện duy nhất. Giúp các sếp tự động hóa quy trình, giảm thiểu rủi ro và tăng cường an toàn cho hệ thống."
slug: "cau-hinh-cong-loai-ai-thong-minh-mcp-claude"
tags: [n8n, automation, ai-rag, devops, api-integration, claude-ai, google-sheets, security]
keywords: [n8n workflow mcp, tự động hóa api bằng ai, claude ai intent verification, gateway api an toàn, audit log cho ai agent, rate limiting cho api]
---

# 🚀 **Cổng Lối AI Thông Minh: Tự Động Hóa Gọi API Bằng Claude AI & MCP Protocol**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, khi các AI Agent (như Claude AI) cần tương tác với hệ thống doanh nghiệp (CRM, ERP, Database, SaaS...), các sếp thường phải:
- **Tạo thủ công API gateway** để kết nối giữa AI và hệ thống backend.
- **Lo lắng về an toàn** khi AI gọi API không kiểm soát (rủi ro tấn công, dữ liệu sai).
- **Không có hệ thống theo dõi** cho các cuộc gọi API, dẫn đến vi phạm chính sách (SOC2, ISO 27001).
- **Phải quản lý thủ công** các quy tắc rate limiting và permission scope.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Tự động hóa gọi API** qua một cổng lối AI thông minh (MCP Gateway).
✅ **Kiểm soát an toàn** bằng Claude AI để xác minh ý định và kiểm tra tham số.
✅ **Theo dõi toàn bộ lịch sử** gọi API trong Google Sheets (audit log).
✅ **Áp dụng rate limiting** để ngăn chặn abuse và bảo vệ hệ thống.
✅ **Hoạt động 24/7** mà không cần code thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian** lên đến **90%** trong việc quản lý API và AI integration.
- **An toàn tuyệt đối** với cơ chế **Claude AI Intent Verification** và **permission scope**.
- **Tuân thủ pháp lý** với **audit log** đầy đủ cho SOC2/ISO 27001.
- **Tăng hiệu suất** với **rate limiting** và **dry run** trước khi thực thi.
- **Hoạt động liên tục** mà không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI CẬP NHẬP**]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản n8n Self-hosted** (để chạy 24/7).
✔ **Google Sheets** (để lưu **Tool Registry**, **Rate Limit Log**, **Audit Log**).
✔ **Anthropic API Key** (để kết nối với **Claude AI**).
✔ **SMTP Credentials** (để gửi **email cảnh báo** khi có cuộc gọi nguy cơ cao).
✔ **API Keys** của hệ thống backend (CRM, ERP, Database...) để gọi trong node `httpRequest`.

👉 **[Đăng ký VPS TinoHost (Self-hosted n8n) với mã giảm giá VPSN8N](https://tino.vn/vps-n8n?affid=388)** (giảm tới **39%**).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13590](https://n8n.io/workflows/13590) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

:::note[**Lưu ý khi import**]
- **Không thay đổi cấu trúc** của workflow (sắp xếp node theo thứ tự ban đầu).
- **Không xóa node** `Wait For Result` (node này đảm bảo workflow không bị treo).
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **🔹 Node 1: Receive MCP Tool Request (Webhook)**
- **Không cần cấu hình** (n8n tự động tạo URL webhook).
- **Lưu ý:** Đảm bảo **HTTP Method = POST** và **Path = `mcp-gateway`**.

#### **🔹 Node 2: Validate Auth and MCP Schema (Code)**
- **Cần điền:**
  - **API Key** (để xác thực yêu cầu gọi API).
  - **JWT Token** (nếu sử dụng).
  - **MCP Schema** (cấu trúc payload phải tuân theo mẫu dưới đây).
- **Mẫu payload yêu cầu:**
  ```json
  {
    "mcpVersion": "1.0",
    "clientId": "agent-crm-001",
    "apiKey": "mcp-key-xxxx",
    "toolName": "crm.get_customer",
    "parameters": { "customerId": "CUST-10042" },
    "requestId": "req-abc-123",
    "callerContext": "User asked: show me customer details"
  }
  ```

#### **🔹 Node 3: Lookup Tool in Registry (Google Sheets)**
- **Cấu hình Google Sheets:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name:** Đặt tên là **"Tool Registry"** (các sếp tự tạo sheet này).
  - **Dữ liệu cần có trong sheet:**
    | Tool Name       | API Endpoint          | Method | Headers (JSON) | Permissions (JSON) |
    |-----------------|-----------------------|--------|----------------|--------------------|
    | `crm.get_customer` | `https://api.crm.com/v1/customers` | GET | `{"Authorization": "Bearer {{API_KEY}}"}` | `{"read": true}` |
    | `erp.update_stock` | `https://api.erp.com/v1/stock` | POST | `{"Content-Type": "application/json"}` | `{"write": true}` |

#### **🔹 Node 4: Claude AI Intent and Safety Verification (Agent + lmChatAnthropic)**
- **Cấu hình Anthropic API:**
  - **Credentials:** Chọn `anthropicApi`.
  - **Model:** `claude-sonnet-4-20250514` (đã được cài đặt sẵn).
  - **Prompt mẫu** (cần chỉnh trong node `Code` trước node `Claude AI Model`):
    ```javascript
    // Kiểm tra ý định và an toàn của request
    const isSafe = data.parameters.customerId.startsWith("CUST-");
    if (!isSafe) throw new Error("Invalid customer ID format!");
    ```
- **Lưu ý:** Nếu Claude AI phát hiện **rủi ro cao**, workflow sẽ **tự động gửi email cảnh báo** (node `Send Security Alert`).

#### **🔹 Node 5: Check Rate Limit and Quota (Google Sheets)**
- **Cấu hình Google Sheets:**
  - **Sheet Name:** **"Rate Limit Log"** (các sếp tự tạo).
  - **Dữ liệu cần có:**
    | Client ID | Tool Name | Max Calls/Day | Calls Used |
    |-----------|-----------|---------------|------------|
    | `agent-crm-001` | `crm.get_customer` | 1000 | 0 |

#### **🔹 Node 6: Execute Backend API Call (httpRequest)**
- **Cấu hình:**
  - **URL:** Được lấy từ **Tool Registry** (node 3).
  - **Method:** GET/POST/PUT/DELETE (tùy tool).
  - **Headers & Body:** Được truyền từ **Resolve Tool Config** (node 5).

#### **🔹 Node 7: Send Security Alert on High Risk Calls (emailSend)**
- **Cấu hình SMTP:**
  - **Credentials:** Chọn `smtp`.
  - **Địa chỉ email:** Cần điền địa chỉ **của quản trị viên** để nhận cảnh báo.
  - **Nội dung email mẫu:**
    ```
    Chủ đề: **Cảnh báo cuộc gọi API nguy cơ cao**
    Nội dung: "Cuộc gọi từ client {{data.clientId}} đến tool {{data.toolName}} bị Claude AI đánh giá là nguy cơ cao. Tham số: {{data.parameters}}"
    ```

#### **🔹 Node 8: Write Immutable Audit Log (Google Sheets)**
- **Cấu hình Google Sheets:**
  - **Sheet Name:** **"Audit Log"** (các sếp tự tạo).
  - **Dữ liệu cần có:**
    | Request ID | Tool Name | Client ID | Timestamp | Status | Response |
    |------------|-----------|-----------|-----------|--------|----------|
    | `req-abc-123` | `crm.get_customer` | `agent-crm-001` | `2024-05-20 10:00:00` | `SUCCESS` | `{"data": {...}}` |

#### **🔹 Node 19: Return MCP Tool Result to Caller (respondToWebhook)**
- **Không cần cấu hình** (n8n tự động trả về kết quả cho client).

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với payload mẫu:
   ```json
   {
     "mcpVersion": "1.0",
     "clientId": "agent-crm-001",
     "apiKey": "mcp-key-12345",
     "toolName": "crm.get_customer",
     "parameters": { "customerId": "CUST-10042" },
     "requestId": "req-test-001",
     "callerContext": "User asked: show me customer details"
   }
   ```
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node `Send Security Alert` để **cảnh báo tức thời** khi có cuộc gọi nguy cơ cao.

### **🔹 Lưu Log vào Database (MySQL/PostgreSQL)**
- Thay thế node `Google Sheets` trong **Audit Log** và **Rate Limit Log** bằng **MySQL/PostgreSQL** để **tăng tốc độ** và **tối ưu hóa**.

### **🔹 Tự Động Gửi Báo Cáo Hàng Ngày**
- Sử dụng **n8n Cron Trigger** để **tổng hợp và gửi báo cáo** về số lượng cuộc gọi API, rate limit, và lỗi xảy ra qua email.

### **🔹 Sử Dụng Multiple Claude Models**
- Thay đổi model Claude trong node `lmChatAnthropic` từ `claude-sonnet-4` sang `claude-instant-1` để **tăng tốc độ** nhưng giảm độ chính xác.

---

## 📌 **Kết Luận**
Workflow **Cổng Lối AI Thông Minh** là giải pháp **tự động hóa API an toàn** với Claude AI, giúp các sếp:
✔ **Tiết kiệm thời gian** trong việc quản lý API.
✔ **Bảo vệ hệ thống** với cơ chế **intent verification** và **rate limiting**.
✔ **Tuân thủ pháp lý** với **audit log** đầy đủ.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**🚀 Hãy cài đặt ngay và tự động hóa hệ thống của mình!**
👉 **[Tải workflow từ n8n.io](https://n8n.io/workflows/13590)** và bắt đầu ngay!