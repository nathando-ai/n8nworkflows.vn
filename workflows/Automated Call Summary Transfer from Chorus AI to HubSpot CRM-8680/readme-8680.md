---
title: "🤖 **Tự Động Hoàn Chỉnh Ghi Chú Cuộc Gọi từ Chorus AI sang HubSpot CRM - Giảm Thời Gian Làm Việc 80%!**"
description: "Workflow tự động hóa chuyển dữ liệu tóm tắt cuộc gọi từ Chorus AI sang HubSpot CRM, giúp các sếp tiết kiệm thời gian, tránh sai sót và đồng bộ hóa thông tin liên tục. Hoạt động 24/7, không cần code!"
slug: "tieu-dong-hoan-chinh-ghi-chu-cuoc-goi-chorus-ai-sang-hubspot"
tags: [n8n, automation, CRM, HubSpot, Chorus AI, no-code, AI CRM]
keywords: [tự động hóa Chorus AI HubSpot, ghi chú cuộc gọi tự động, CRM tự động, workflow n8n CRM, đồng bộ hóa cuộc gọi, tiết kiệm thời gian bán hàng]
---

# 🚀 **Tự Động Hoàn Chỉnh Ghi Chú Cuộc Gọi từ Chorus AI sang HubSpot CRM**

### **Giải Phóng Tay Các Sếp: Từ Ghi Chú Thủ Công sang Tự Động Hóa 100%**
Hiện nay, các sếp và đội ngũ bán hàng thường phải tốn **giờ đồng hồ** để ghi chép lại nội dung cuộc gọi từ Chorus AI vào HubSpot CRM. Điều này không chỉ **tốn thời gian** mà còn dễ gây **sai sót** khi ghi nhớ không chính xác. Với workflow này, các sếp sẽ **tự động hóa toàn bộ quy trình**, đồng bộ hóa ghi chú cuộc gọi từ Chorus AI sang HubSpot **mỗi giờ một lần**, giúp:
- **Tiết kiệm 80% thời gian** ghi chép thủ công.
- **Đồng bộ hóa dữ liệu chính xác**, tránh mất mát thông tin.
- **Cập nhật liên tục** (hoạt động 24/7).
- **Tăng cường hiệu quả bán hàng** với ghi chú chi tiết và cá nhân hóa.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần phải ghi chép lại cuộc gọi thủ công.
✅ **Dữ liệu chính xác**: Tránh sai sót khi nhập liệu.
✅ **Hoạt động liên tục**: Cập nhật ghi chú mỗi giờ tự động.
✅ **Tích hợp AI & CRM**: Sử dụng Chorus AI (AI ghi chú cuộc gọi) + HubSpot (CRM chuyên nghiệp).
✅ **Tự động hóa hoàn chỉnh**: Không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Chorus AI** với **API Key** để truy cập dữ liệu cuộc gọi.
2. **Tài khoản HubSpot** với:
   - **App Token** (để kết nối API).
   - **Tên công ty** trong HubSpot phải **trùng khớp** với `account_name` trong Chorus AI.
3. **VPS hoặc máy chủ** để chạy n8n (khuyến nghị **Self-hosted**).
4. **Thời gian** để cấu hình và test workflow.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/8680](https://n8n.io/workflows/8680) hoặc sao chép **JSON** từ trang này.
- **Bước 2**: Mở **n8n Editor** và chọn **"Import Workflow"** → Dán JSON hoặc tải file `.json`.
- **Bước 3**: Chọn **"Active"** để kích hoạt workflow.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **15 node** với logic phức tạp. Các sếp cần chú ý cấu hình **các node sau**:

##### **🔹 Node "Get Chorus Engagement per last day" (HTTP Request)**
- **Mục đích**: Lấy dữ liệu cuộc gọi mới nhất từ Chorus AI trong **1 ngày**.
- **Cấu hình**:
  - **URL**: `https://api.chorus.ai/v1/engagements` (cần kiểm tra API chính xác của Chorus AI).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_CHORUS_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Query Parameters**:
    ```json
    {
      "limit": 100,
      "offset": 0,
      "filter": "created_at > now-1d"
    }
    ```
  - **Lưu ý**: Nếu Chorus AI hỗ trợ **pagination**, cần cấu hình `offset` để lấy toàn bộ dữ liệu.

##### **🔹 Node "Merge paginated engagements" (Code)**
- **Mục đích**: Ghép dữ liệu từ nhiều trang (nếu có pagination).
- **Mã JavaScript**:
  ```javascript
  // Kiểm tra nếu có pagination và ghép dữ liệu
  const engagements = $input.all();
  const mergedEngagements = [];

  // Nếu có nhiều trang, ghép vào mergedEngagements
  engagements.forEach((engagementBatch) => {
    mergedEngagements.push(...engagementBatch.json);
  });

  return { json: mergedEngagements };
  ```

##### **🔹 Node "Filter items with empty meeting_summary" (Filter)**
- **Mục đích**: Loại bỏ cuộc gọi **không có ghi chú** (`meeting_summary` trống).
- **Cấu hình**:
  - **Condition**: `{{ $json.meeting_summary }} == ""` → **Exclude**.

##### **🔹 Node "Search Company In HubSpot By Name" (HTTP Request)**
- **Mục đích**: Tìm công ty trong HubSpot **trùng khớp** với `account_name` từ Chorus AI.
- **Cấu hình**:
  - **URL**: `https://api.hubapi.com/crm/v3/objects/companies/search`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_HUBSPOT_APP_TOKEN",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "properties": [
        {
          "name": "name",
          "value": "{{ $json.account_name }}"
        }
      ]
    }
    ```

##### **🔹 Node "If company exists" (If)**
- **Mục đích**: Kiểm tra nếu công ty **tồn tại** trong HubSpot.
- **Cấu hình**:
  - **Condition**: `{{ $json.results.length > 0 }}` → **True**.

##### **🔹 Node "Search notes" (HTTP Request)**
- **Mục đích**: Kiểm tra nếu **ghi chú cuộc gọi đã tồn tại** trong HubSpot.
- **Cấu hình**:
  - **URL**: `https://api.hubapi.com/crm/v3/objects/notes/search`
  - **Headers**: (Giống như trên).
  - **Body**:
    ```json
    {
      "properties": [
        {
          "name": "associated_object_id",
          "value": "{{ $json.results[0].id }}"
        },
        {
          "name": "content",
          "value": "{{ $json.meeting_summary }}"
        }
      ]
    }
    ```

##### **🔹 Node "Create Note Payload" (Code)**
- **Mục đích**: Tạo **payload** cho ghi chú mới trong HubSpot.
- **Mã JavaScript**:
  ```javascript
  return {
    json: {
      properties: {
        associated_object_id: "{{ $json.results[0].id }}",
        content: "{{ $json.meeting_summary }}",
        title: `Ghi chú cuộc gọi từ Chorus AI - ${new Date($json.created_at).toLocaleString()}`
      }
    }
  };
  ```

##### **🔹 Node "Create Note" (HTTP Request)**
- **Mục đích**: Tạo ghi chú mới trong HubSpot.
- **Cấu hình**:
  - **URL**: `https://api.hubapi.com/crm/v3/objects/notes`
  - **Headers**: (Giống như trên).
  - **Body**: Sử dụng kết quả từ `Create Note Payload`.

##### **🔹 Node "Run every hour" (Schedule Trigger)**
- **Mục đích**: Chạy workflow **mỗi giờ một lần**.
- **Cấu hình**:
  - **Schedule**: `0 * * * *` (mỗi giờ).

##### **🔹 Node "When clicking ‘Execute workflow’" (Manual Trigger)**
- **Mục đích**: Cho phép **kích hoạt thủ công** nếu cần.

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Test run với **dữ liệu mẫu** từ Chorus AI.
- **Bước 2**: Kiểm tra **ghi chú đã được tạo** trong HubSpot.
- **Bước 3**: Bật **Active workflow** và **đợi nó chạy tự động**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có ghi chú mới được tạo.
   - **Cách làm**:
     ```json
     {
       "name": "Notify on Slack",
       "type": "httpRequest",
       "method": "POST",
       "url": "https://hooks.slack.com/services/YOUR_SLACK_WEBHOOK",
       "body": {
         "text": `Ghi chú mới được tạo cho công ty: {{ $json.account_name }}`
       }
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại **lịch sử hoạt động** của workflow.
   - **Cách làm**:
     ```json
     {
       "name": "Log to Google Sheets",
       "type": "googleSheets",
       "operation": "createRow",
       "sheetName": "Workflow_Log",
       "credentials": ["googleSheets"],
       "body": {
         "values": [
           {
             "companyName": "{{ $json.account_name }}",
             "noteCreated": "{{ $json.created_at }}",
             "status": "Success"
           }
         ]
       }
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node Schedule Trigger** để gửi **báo cáo tổng hợp** về số lượng ghi chú được tạo mỗi ngày.
   - **Cách làm**:
     - Thêm node **Email** (n8n-nodes-base.email) hoặc **Google Drive** để lưu báo cáo.

4. **Xử lý lỗi tự động**:
   - Thêm node **Set** để lưu **lỗi** vào biến và gửi thông báo qua **Slack/Email**.
   - **Cách làm**:
     ```json
     {
       "name": "Handle Errors",
       "type": "set",
       "variables": {
         "lastError": "{{ $error.message }}"
       }
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng tay các sếp** khỏi công việc ghi chú thủ công, đồng thời **tăng cường hiệu quả bán hàng** bằng cách tự động hóa quy trình đồng bộ hóa dữ liệu giữa **Chorus AI và HubSpot**. Với **tính năng chạy tự động mỗi giờ**, các sếp không cần lo lắng về việc **mất mát thông tin** hoặc **sai sót** khi nhập liệu.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình API keys** và test.
3. **Bật hoạt động tự động** và **giải phóng thời gian** cho công việc quan trọng hơn!

---
**💡 Cần hỗ trợ thêm?**
- Liên hệ tác giả **Rivers Colyer** trên [LinkedIn](https://www.linkedin.com/in/rivercolyer/) để yêu cầu **cấu hình workflow riêng**.
- Đăng ký **VPS n8n** để chạy ổn định: [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**).