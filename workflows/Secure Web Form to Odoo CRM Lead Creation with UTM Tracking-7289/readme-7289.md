---
title: "🚀 Tự Động Hóa Form Báo Danh An Toàn → Tạo Lead CRM Odoo Với Theo Dõi UTM (N8n)"
description: "Workflow này tự động chuyển đổi dữ liệu từ form báo danh an toàn thành lead CRM trong Odoo, đồng thời theo dõi nguồn traffic (UTM) từ quảng cáo. Giúp các sếp tiết kiệm thời gian, giảm sai sót và tối ưu hóa chiến dịch marketing."
slug: "tieu-dong-hoa-form-bao-danh-ano-toan-den-odoo-crm-voi-utm"
tags: [n8n, automation, odoo, lead-generation, utm-tracking, no-code]
keywords: [n8n workflow odoo, tự động hóa form báo danh, theo dõi utm trong odoo, tự động hóa crm, n8n lead generation]
---

# 🚀 **Tự Động Hóa Form Báo Danh An Toàn → Tạo Lead CRM Odoo Với Theo Dõi UTM**

### **Giải pháp cho các sếp:**
Hết sức phiền phức phải nhập liệu thủ công từ form báo danh an toàn vào Odoo CRM? Hay phải theo dõi nguồn traffic từ quảng cáo (UTM) để phân tích hiệu quả? **Workflow này tự động hóa toàn bộ quy trình**, giúp bạn:
- **Tiết kiệm 100% thời gian** nhập liệu thủ công.
- **Chuyển đổi lead chính xác** với thông tin đầy đủ (tên, email, số điện thoại, ghi chú).
- **Theo dõi nguồn traffic** (source, medium, campaign) từ UTM để tối ưu hóa chiến dịch marketing.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa nhập liệu**: Dữ liệu từ form báo danh an toàn được chuyển trực tiếp vào Odoo CRM.
- **Theo dõi UTM chính xác**: Nguồn traffic (source, medium, campaign) được gắn vào lead, giúp phân tích hiệu quả quảng cáo.
- **Chất lượng lead cao**: Dữ liệu được kiểm tra và chuẩn hóa trước khi tạo lead.
- **Hoạt động liên tục**: Workflow chạy tự động mà không cần can thiệp của con người.
- **Giảm sai sót**: Không còn lỗi nhập liệu thủ công, dữ liệu luôn chính xác.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Odoo**:
   - Đã kích hoạt tính năng **Lead (CRM)** trong Odoo (CRM → Settings → Leads).
   - **API Key** của người dùng Odoo (sử dụng làm mật khẩu).
2. **Thông tin kết nối Odoo**:
   - **URL Odoo** (ví dụ: `https://your-odoo-domain.com`).
   - **Tên cơ sở dữ liệu (DB name)**.
   - **Tên đăng nhập (Login)** và **API Key**.
3. **Webhook**:
   - **URL công khai** cho webhook (sử dụng ngrok, Cloudflare, hoặc reverse proxy).
   - **Header Auth**: Thiết lập một secret cho header, ví dụ: `x-webhook-token: {{$env.WEBHOOK_SECRET}}`.
4. **Dữ liệu UTM trong Odoo**:
   - Các trường **utm.source**, **utm.medium**, **utm.campaign** phải được tạo trong Odoo (nếu chưa có, cần tạo trước).
5. **n8n**:
   - Tài khoản n8n đã cài đặt và chạy (self-hosted hoặc cloud).
   - **Credentials Odoo** đã được cấu hình trong n8n.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/7289).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Webhook - Lead Webform**
- **Credentials**: Chọn `httpHeaderAuth` (đã thiết lập secret trong header).
- **Key Parameters**:
  - `path`: `lead-webform` (để trùng với endpoint test/prod).
  - `httpMethod`: `POST`.

##### **B. Odoo Credentials**
- **Credentials**: Chọn `odooApi` (đã cấu hình trước trong n8n).
- **Resource**: Đảm bảo đã chọn `custom` (đối với lead).

##### **C. UTM Lookup (3 node)**
Các node này sẽ tìm kiếm **ID** của `utm.source`, `utm.medium`, `utm.campaign` trong Odoo:
- **Operation**: `getAll`.
- **Resource**: `custom`.
- **Lưu ý**:
  - Nếu trường UTM chưa tồn tại trong Odoo, workflow sẽ tự động đặt `null` (an toàn).
  - Các sếp cần đảm bảo các trường này đã được tạo trong Odoo trước khi chạy workflow.

##### **D. Code Node (Prepare Request)**
- **Lưu ý**: Node này sẽ **merge** dữ liệu từ webhook và UTM lookup thành một object chuẩn cho Odoo.
- **Cấu trúc output**:
  ```json
  {
    "name": "{{$json["firstname"]}} {{$json["lastname"]}}",
    "contact_name": "{{$json["email"]}}",
    "email_from": "{{$json["email"]}}",
    "phone": "{{$json["phone"]}}",
    "description": "{{$json["notes"]}}",
    "type": "lead",
    "campaign_id": "{{$node["UTM: Get Campaign ID"].json[0].id}}",
    "source_id": "{{$node["UTM: Get Source ID"].json[0].id}}",
    "medium_id": "{{$node["UTM: Get Medium ID"].json[0].id}}"
  }
  ```

##### **E. Validation (3 node Code)**
- **Source ID Validation**, **Medium ID Validation**, **Campaign ID Validation**:
  - Các node này sẽ **kiểm tra** xem ID UTM có tồn tại không.
  - Nếu không tồn tại, workflow sẽ tự động đặt `null` (không cần xử lý thêm).

##### **F. Respond to Webhook**
- **Success**: Trả về `200 OK` với thông tin lead đã tạo.
- **Bad Request**: Trả về `400` nếu dữ liệu thiếu hoặc không hợp lệ.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một request mẫu đến webhook để kiểm tra:
     ```bash
     curl -X POST "https://<host>/webhook-test/lead-webform" \
       -H "Content-Type: application/json" \
       -H "x-webhook-token: <secret>" \
       -d '{"firstname":"John","lastname":"Doe","email":"john@ex.com",
            "phone":"+393331212123", "notes":"Demo",
            "source":"Ads","medium":"Website","campaign":"Spring 2025"}'
     ```
   - Kiểm tra kết quả trong Odoo và log của n8n.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi lead mới**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **Create Lead** để thông báo lead mới.
2. **Lưu log hoạt động**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử lead đã tạo.
3. **Tự động tạo UTM nếu thiếu**:
   - Thêm node **IF** sau mỗi `getAll` UTM, nếu không tìm thấy ID, tự động tạo mới.
4. **Gửi email xác nhận cho lead**:
   - Thêm node **Email** (ví dụ: SendGrid) sau node **Create Lead** để gửi email cảm ơn.
5. **Tích hợp với Google Analytics**:
   - Sử dụng API Google Analytics để lấy dữ liệu traffic chi tiết và gắn vào lead.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình báo danh an toàn và theo dõi hiệu quả quảng cáo. Bằng cách kết hợp **n8n** với **Odoo**, bạn không chỉ tiết kiệm thời gian mà còn đảm bảo dữ liệu lead được quản lý chính xác và hiệu quả.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động ổn định.
3. **Bật Active** và bắt đầu tự động hóa!

Nếu có bất kỳ vấn đề nào, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n để được hỗ trợ. **Chúc các sếp thành công!** 🚀