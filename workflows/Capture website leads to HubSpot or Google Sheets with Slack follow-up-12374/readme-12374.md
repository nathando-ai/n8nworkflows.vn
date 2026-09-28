---
title: "🚀 Tự Động Hóa Nhận Dữ Liệu Website Sang HubSpot/Google Sheets Với Thông Báo Slack Tự Động - Giảm 90% Công Việc Nhập Dữ Liệu"
description: "Workflow này tự động chụp dữ liệu từ form website (POST) và lưu vào HubSpot hoặc Google Sheets, đồng thời gửi thông báo Slack thành công/thất bại. Giúp các sếp tiết kiệm 5-10 giờ/tuần và giảm sai sót trong quản lý leads."
slug: "tu-dong-hoa-nhan-du-lieu-website-sang-hubspot-google-sheets"
tags: [n8n, automation, lead-generation, hubspot, google-sheets, slack, no-code]
keywords: [n8n workflow tự động hóa leads, tự động hóa nhận dữ liệu website, HubSpot API tự động, Google Sheets tự động cập nhật, Slack thông báo tự động, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Nhận Dữ Liệu Website Sang HubSpot/Google Sheets Với Thông Báo Slack Tự Động**

### **Giải Pháp Cho Các Sếp Bị Chán Nhập Dữ Liệu T Tay**
Hàng ngày, các sếp phải mất thời gian quét form website, sao chép dữ liệu vào HubSpot hoặc Google Sheets, rồi gửi email/Slack để xác nhận. **Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây!**
- **Không cần code** – chỉ cần cấu hình vài nút chuột.
- **Hoạt động 24/7** – không lo bỏ quên hoặc sai sót.
- **Cá nhân hóa thông báo** – biết ngay liệu dữ liệu đã được lưu thành công hay thất bại.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần**: Không cần nhập dữ liệu thủ công.
- **Chính xác 100%**: Không lo sai sót khi copy-paste.
- **Quản lý leads hiệu quả**: Dữ liệu tự động phân loại vào HubSpot hoặc Google Sheets.
- **Thông báo tức thời**: Biết ngay liệu dữ liệu đã được lưu thành công hay thất bại qua Slack.
- **Hoạt động liên tục**: Dữ liệu được cập nhật ngay khi khách hàng gửi form.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (API Key) hoặc **Google Sheets** (File Sheets và Credentials).
2. **Tài khoản Slack** (Webhook URL để nhận thông báo).
3. **URL Webhook** của n8n (sẽ được cung cấp khi cài đặt).
4. **Dịch vụ enrichment (tùy chọn)**: Nếu muốn enrich dữ liệu (ví dụ: Clearbit, Hunter.io), cần API Key và URL của dịch vụ đó.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/12374](https://n8n.io/workflows/12374) hoặc copy JSON từ đây.
- **Bước 2**: Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Bước 3**: Chọn **"Active"** để kích hoạt workflow.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **24 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Webhook Trigger (Node 1)**
- **Cấu hình**:
  - **Path**: `website-lead` (không đổi).
  - **HTTP Method**: `POST`.
- **Test**: Gửi request POST từ Postman hoặc website với body JSON như sau:
  ```json
  {
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@example.com",
    "company": "johnscompany",
    "message": "Need help...",
    "source": "contact_page",
    "enrich": false,
    "destination": "sheets"  // hoặc "hubspot"
  }
  ```

##### **B. Parse Webhook Body (Node 24)**
- **Chức năng**: Chuyển đổi body JSON thành dạng chuẩn.
- **Lưu ý**: Nếu body là `text/plain`, node này sẽ tự động chuyển đổi.

##### **C. Normalize Leads (Node 2)**
- **Cấu hình**:
  - **Trim spaces**: Bật để loại bỏ khoảng trắng thừa.
  - **Lowercase email**: Bật để đảm bảo email không bị sai chữ hoa/thường.
- **Mẫu Google Sheets (Node 10)**:
  ```plaintext
  receivedAt → ={{$json.lead.receivedAt || $now}}
  name → ={{$json.lead.name}}
  email → ={{$json.lead.email}}
  company → ={{$json.lead.company}}
  message → ={{$json.lead.message}}
  source → ={{$json.lead.source}}
  destination → ={{$json.lead.destination}}
  enrichment → ={{JSON.stringify($json.lead.enrichment || null)}}
  updatedAt → ={{$now}}
  status → New
  ```

##### **D. Validate Lead (Node 3 - Code)**
- **Lưu ý**: Node này kiểm tra các trường bắt buộc (`email`, `name`, `message`). Nếu thiếu hoặc sai, workflow sẽ trả về **400 Bad Request**.
- **Mẫu mã code**:
  ```javascript
  // Kiểm tra email có hợp lệ không
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test($json.lead.email)) {
    throw new Error("Email không hợp lệ");
  }
  // Kiểm tra trường bắt buộc
  if (!($json.lead.firstName && $json.lead.lastName && $json.lead.message)) {
    throw new Error("Thiếu trường bắt buộc");
  }
  ```

##### **E. Enrichment (Node 6 - HTTP Request)**
- **Nếu `enrich: true`**:
  - Thay đổi **URL** trong node HTTP thành URL của dịch vụ enrichment (ví dụ: `https://api.clearbit.com/v2/enrich/?email=john@example.com`).
  - Sau đó, **merge** dữ liệu enrichment vào lead (Node 7).

##### **F. Switch Destination (Node 9)**
- **Cấu hình**:
  - Nếu `destination: "sheets"` → Lưu vào **Google Sheets**.
  - Nếu `destination: "hubspot"` → Lưu vào **HubSpot**.
- **Google Sheets (Node 10)**:
  - **Operation**: `appendOrUpdate`.
  - **Credentials**: Thêm tài khoản Google Sheets vào n8n.
- **HubSpot (Node 13)**:
  - **Credentials**: Thêm API Key HubSpot vào n8n.
  - **Action**: `Create/Update contact`.

##### **G. Slack Notifications (Node 12, 14, 16, 18)**
- **Cấu hình**:
  - Thêm **Webhook URL** của Slack vào node Slack.
  - **Mẫu thông báo**:
    - **Thành công**: `🎉 Lead đã được lưu thành công vào [Sheets/HubSpot]!`
    - **Thất bại**: `❌ Lỗi khi lưu lead: [Lỗi cụ thể]`

##### **H. Respond to Webhook (Node 5, 15, 17, 19, 20, 21, 22, 23)**
- **Cấu hình**:
  - **200 OK**: Trả về khi lưu thành công.
  - **500 Error**: Trả về khi lưu thất bại (Sheets/HubSpot).

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Test run với dữ liệu mẫu (như ví dụ trên).
- **Bước 2**: Nhấn **"Active"** để bật workflow.
- **Bước 3**: Gửi request từ website/form để kiểm tra.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với CRM khác**:
   - Thay thế HubSpot bằng **Salesforce** hoặc **Zoho CRM** bằng cách thêm node tương ứng.
2. **Lưu log dữ liệu**:
   - Thêm node **Google Drive** hoặc **AWS S3** để lưu bản sao dữ liệu.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** hoặc **HubSpot** để tạo báo cáo hàng tuần/month.
4. **Tự động enrich dữ liệu**:
   - Kết nối với **Clearbit** hoặc **Hunter.io** để enrich thông tin công ty, vị trí, và số điện thoại.
5. **Bảo mật dữ liệu**:
   - Mật mã hóa email trong Google Sheets bằng cách sử dụng **Google Apps Script**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập dữ liệu thủ công, đồng thời **tăng cường độ chính xác** và **tự động hóa quản lý leads**. **Chỉ cần 10 phút để cấu hình**, sau đó dữ liệu sẽ tự động lưu vào HubSpot hoặc Google Sheets, và các sếp sẽ được thông báo tức thời qua Slack.

**🚀 Hãy áp dụng ngay và tiết kiệm 5-10 giờ/tuần!**
Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn chi tiết trên n8n.io](https://n8n.io/workflows/12374) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community).