---
title: "🚀 Tự Động Hoá Gửi Email Bán Hàng Cá Nhân Hóa Theo Sản Phẩm Mới Ra Mắt Với AI Claude & Explorium (N8N)"
description: "Workflow tự động hóa gửi email bán hàng cá nhân hóa dựa trên thông tin sản phẩm mới ra mắt, kết hợp AI Claude 3.7 Sonnet và công cụ nghiên cứu Explorium để tăng tỷ lệ phản hồi và chuyển đổi. Giúp các sếp tiết kiệm thời gian lên đến 80% trong công việc outreach."
slug: "tieu-dong-hoa-gui-email-ban-hang-ca-nhan-hoa-voi-claude-explorium"
tags: [n8n, automation, sales, ai, claude-3, explorium, no-code]
keywords: [n8n workflow bán hàng, tự động hóa email cá nhân hóa, AI Claude 3.7 Sonnet, Explorium MCP, outreach tự động, tăng tỷ lệ chuyển đổi]
---

# 🚀 **Tự Động Hoá Email Bán Hàng Cá Nhân Hóa Theo Sản Phẩm Mới Ra Mắt Với AI Claude & Explorium**

## **📌 Nỗi Đau Của Các Sếp Trong Outreach Bán Hàng**
Gửi email bán hàng thủ công không chỉ tốn thời gian mà còn dễ gây cảm giác **lặp đi lặp lại** và **không cá nhân hóa**. Các sếp phải:
- **Tìm kiếm thông tin** về khách hàng tiềm năng (công ty, nhân viên, sở thích).
- **Viết email riêng biệt** cho từng cá nhân, dẫn đến **tỷ lệ mở thấp** và **chuyển đổi kém**.
- **Phản hồi chậm** khi khách hàng không có dữ liệu chi tiết.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Tự động nghiên cứu** thông tin công ty và nhân viên từ Explorium.
✅ **Sử dụng AI Claude 3.7 Sonnet** để viết email **cá nhân hóa 100%**.
✅ **Gửi email ngay lập tức** qua Slack hoặc email (có thể mở rộng).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 80% thời gian** so với viết email thủ công.
- **Tỷ lệ mở email tăng 3-5 lần** nhờ nội dung cá nhân hóa.
- **Chuyển đổi cao hơn** vì email phù hợp với từng cá nhân.
- **Hoạt động liên tục** mà không cần can thiệp.
- **Dễ mở rộng** cho nhiều sản phẩm mới ra mắt.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản n8n Self-hosted** (khuyến nghị dùng VPS để chạy 24/7).
2. **API Keys & Credentials**:
   - **Explorium MCP API Key** (để nghiên cứu công ty và nhân viên).
   - **Anthropic API Key** (để sử dụng Claude 3.7 Sonnet).
   - **Slack OAuth2 Token** (để gửi kết quả ra Slack).
   - **Nếu muốn mở rộng**: Tài khoản email (SMTP) hoặc API email (SendGrid, Mailgun).
3. **Dữ liệu đầu vào**:
   - **Thông tin sản phẩm mới ra mắt** (tên, mô tả, liên kết).
   - **Danh sách công ty tiềm năng** (có thể lấy từ LinkedIn, CRM, hoặc nhập thủ công).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4711](https://n8n.io/workflows/4711).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste JSON** vào **Create New Workflow** → **Import from JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1: Nghiên cứu công ty & nhân viên** (sử dụng Explorium).
- **Phần 2: Viết email cá nhân hóa** (sử dụng AI Claude).

##### **A. Cấu Hình Webhook (Đầu vào)**
- **Node: Webhook**
  - **Path**: `https://lievi.app.n8n.cloud/webhook-test/product-launch`
  - **HTTP Method**: `POST`
  - **Lưu ý**:
    - Nếu tự host, thay đổi **path** thành URL của VPS cá nhân.
    - **Test Webhook** bằng cách gửi request JSON mẫu:
      ```json
      {
        "product_name": "Sản phẩm mới XYZ",
        "product_description": "Mô tả chi tiết sản phẩm...",
        "company_list": ["Công ty A", "Công ty B"]
      }
      ```

##### **B. Cấu Hình Explorium MCP (Nghiên cứu công ty)**
- **Node: Explorium MCP**
  - **Credentials**: Chọn `httpBearerAuth` (đã cấu hình API Key Explorium).
  - **Key Parameters**:
    - **Endpoint**: `https://api.explorium.com/v1/research` (thay đổi nếu khác).
    - **Query**: `"company_name": "{{$node["Webhook"].json["$.company_list"]}}"` (lấy danh sách công ty từ Webhook).

##### **C. Cấu Hình AI Claude 3.7 Sonnet (Viết email)**
- **Node: Anthropic Chat Model (3 node)**
  - **Credentials**: Chọn `anthropicApi` (đã cấu hình API Key Claude).
  - **Model**: `claude-3-7-sonnet-20250219` (đã được cache).
  - **Prompt mẫu** (cần chỉnh sửa theo yêu cầu):
    ```plaintext
    Bạn là một chuyên gia viết email bán hàng. Dựa trên thông tin sau:
    - Sản phẩm: {{$node["Webhook"].json["$.product_name"]}}
    - Mô tả sản phẩm: {{$node["Webhook"].json["$.product_description"]}}
    - Thông tin công ty: {{$node["Explorium MCP"].json["$.company_data"]}}
    Viết một email cá nhân hóa cho nhân viên {{$node["Prospect Fetcher"].json["$.employee_name"]}} tại {{$node["Prospect Fetcher"].json["$.company_name"]}}.
    ```
  - **Lưu ý**:
    - **Node "Email Writer (YES prospect data)"** → Dùng khi có dữ liệu nhân viên.
    - **Node "Email Writer (NO prospect data)"** → Dùng khi không tìm thấy dữ liệu.

##### **D. Cấu Hình Slack Output (Gửi kết quả)**
- **Node: Slack Output (2 node)**
  - **Credentials**: Chọn `slackOAuth2Api` (đã cấu hình token Slack).
  - **Channel**: Chọn kênh Slack muốn gửi kết quả.
  - **Message Format**:
    ```plaintext
    🚀 **Email cá nhân hóa cho {{$node["Prospect Fetcher"].json["$.employee_name"]}}**
    - Công ty: {{$node["Prospect Fetcher"].json["$.company_name"]}}
    - Email: {{$node["Email Writer"].json["$.email_content"]}}
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi request Webhook mẫu (như trên).
  - Kiểm tra **Slack** xem có nhận được email cá nhân hóa không.
- **Bật Active**:
  - Chuyển trạng thái workflow từ **Draft** → **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Mở rộng sang Email (SMTP)**
   - Thêm **Node `n8n-nodes-base.email`** sau Slack để gửi email thực tế.
   - Cấu hình **SMTP** (Gmail, SendGrid, Mailgun).

2. **Lưu Log & Theo Dõi**
   - Thêm **Node `n8n-nodes-base.googleSheets`** để lưu tất cả email đã gửi vào Google Sheets.
   - Cấu hình **Sheet Name** và **Credentials**.

3. **Tích Hợp CRM (HubSpot, Salesforce)**
   - Sử dụng **Node `n8n-nodes-base.httpRequest`** để lấy danh sách khách hàng từ CRM.
   - Thay thế **Webhook** bằng **Trigger từ CRM**.

4. **Cá Nhân Hóa Nhiều Giống**
   - Thêm **Node `n8n-nodes-base.splitInBatches`** để xử lý nhiều sản phẩm cùng lúc.

5. **Dùng Telegram Bot Thay Slack**
   - Thay **Slack Output** bằng **Node `n8n-nodes-base.telegram`** để gửi tin nhắn Telegram.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc viết email thủ công, đồng thời **tăng tỷ lệ chuyển đổi** nhờ nội dung cá nhân hóa. **Chỉ cần 10 phút setup**, workflow sẽ hoạt động tự động 24/7!

**👉 Bắt đầu ngay bằng cách:**
1. **Import workflow** từ [n8n.io/workflows/4711](https://n8n.io/workflows/4711).
2. **Cấu hình API Keys** (Explorium, Claude, Slack).
3. **Test Webhook** và **bật Active**.

**🎁 Đăng ký VPS TinoHost để tự host n8n 24/7 (giảm 39%)**:
👉 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)

---
**💡 Cần hỗ trợ thêm?** Để lại comment bên dưới hoặc liên hệ với tôi! 🚀