---
title: "🚀 Tạo API REST CRUD Siêu Nhanh với Google Sheets (Không Code, 100% Tự Động Hóa)"
description: "Workflow này giúp các sếp xây dựng một API REST đầy đủ chức năng (Create, Read, Update, Delete) chỉ với Google Sheets làm cơ sở dữ liệu, hoàn toàn không cần viết code. Giúp tiết kiệm thời gian phát triển backend lên đến 90% so với cách truyền thống."
slug: "tao-api-rest-crud-voi-google-sheets"
tags: [n8n, automation, no-code, google-sheets, api-rest, backend, crud]
keywords: [n8n workflow google sheets, tự động hóa api rest, backend không code, google sheets làm database, api crud tự động]
---

# 🚀 **Tạo API REST CRUD với Google Sheets (Không Code, Chỉ Cần 10 Min)**

## **🔥 Tại sao các sếp nên dùng workflow này?**
Hiện nay, việc xây dựng backend cho ứng dụng, prototype hoặc công cụ nội bộ thường tốn thời gian và chi phí cao. Các sếp phải viết code, quản lý server, hoặc phải phụ thuộc vào các nhà phát triển. **Workflow này giải quyết vấn đề đó bằng cách:**
- **Tạo API REST đầy đủ CRUD** (Create, Read, Update, Delete) chỉ với **Google Sheets** làm cơ sở dữ liệu.
- **Không cần viết code** – hoàn toàn tự động hóa với n8n.
- **Hoạt động 24/7** – không cần quản lý server, chỉ cần một VPS nhỏ.
- **Dễ dàng mở rộng** – có thể kết nối với Slack, Telegram, hoặc gửi báo cáo tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian phát triển backend** lên đến **90%** so với cách truyền thống.
✅ **Không cần viết code** – chỉ cần cấu hình workflow.
✅ **Dữ liệu luôn đồng bộ** với Google Sheets, dễ dàng quản lý và cập nhật.
✅ **Hoạt động liên tục 24/7** – không cần can thiệp thủ công.
✅ **Mở rộng dễ dàng** – có thể kết nối với Slack, Telegram, hoặc gửi báo cáo tự động.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **Google Sheet** với các cột: `name`, `email`, `status` (hoặc tùy chỉnh theo nhu cầu).
   - **Lưu ý:** Các sếp có thể sử dụng [mẫu Google Sheet này](https://docs.google.com/spreadsheets/d/1bQyl8pGVutkq1LRwK_-6TAAcXwNj4_TipeWHi-qmK1Q/edit?usp=sharing) làm tham khảo.
3. **VPS hoặc máy chủ n8n** (nếu tự host).
4. **API Key của Google Sheets** (được tạo khi kết nối tài khoản Google trong n8n).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/8085) (nếu có link JSON).
2. Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON.
   **Hoặc:**
   - Copy toàn bộ JSON từ [n8n.io/workflows/8085](https://n8n.io/workflows/8085) (ấn **Export**).
   - Dán vào **n8n Editor** và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **🔹 Cấu hình Google Sheets**
1. **Tạo credentials Google API**:
   - Trong **n8n**, đi đến **Credentials** → **Add Credentials** → **Google Sheets**.
   - Đăng nhập tài khoản Google và cấp quyền cho n8n.
   - Lưu credentials với tên `googleApi`.

2. **Chỉnh các node Google Sheets**:
   - **Append row in sheet**: Chọn `googleApi` trong **Credentials** và chọn **Google Sheet** + **Sheet Name**.
   - **Get rows in sheet**: Chọn `googleApi` và chọn **Sheet Name**.
   - **Get row in sheet**: Chọn `googleApi` và **Sheet Name**.
   - **Update row in sheet**: Chọn `googleApi` và **Sheet Name**.
   - **Delete rows or columns from sheet**: Chọn `googleApi` và **Sheet Name**.

##### **🔹 Cấu hình Webhook**
- Các node **Webhook** đã được cấu hình sẵn với các path:
  - `POST /items` (Create)
  - `GET /items/all` (Read All)
  - `GET /items` (Read Single)
  - `PUT /items` (Update)
  - `DELETE /items` (Delete)
- **Không cần chỉnh gì** nếu các sếp muốn sử dụng mặc định.

##### **🔹 Cấu hình "Prepare Fields for Update"**
- Node này **chỉnh sửa dữ liệu trước khi update** vào Google Sheets.
- Các sếp có thể **xóa hoặc chỉnh sửa** các trường không cần thiết trong **JSON Path**.

##### **🔹 Test Webhook**
- Sau khi cấu hình xong, các sếp có thể **test** với các command `curl` sau:
  ```bash
  # POST (Create)
  curl -X POST YOUR_N8N_WEBHOOK_URL/items \
       -H "Content-Type: application/json" \
       -d '{"name": "Alice", "email": "alice@example.com", "status": "active"}'

  # GET (Read All)
  curl -X GET YOUR_N8N_WEBHOOK_URL/items/all

  # GET (Read Single)
  curl -X GET YOUR_N8N_WEBHOOK_URL/items?id=2

  # PUT (Update)
  curl -X PUT YOUR_N8N_WEBHOOK_URL/items?id=2 \
       -H "Content-Type: application/json" \
       -d '{"status": "inactive"}'

  # DELETE (Delete)
  curl -X DELETE YOUR_N8N_WEBHOOK_URL/items?id=2
  ```
- **Thay `YOUR_N8N_WEBHOOK_URL` bằng URL Webhook của n8n** (có thể tìm trong **Settings** → **Webhooks**).

#### **3. Kích hoạt ⚡️**
- Sau khi cấu hình xong, **bật Active** workflow.
- **Test lại** với các command `curl` để đảm bảo hoạt động đúng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có thay đổi dữ liệu.
   - Ví dụ: Khi có dữ liệu mới được tạo (`POST`), gửi thông báo đến Slack.

2. **Lưu log hoạt động**:
   - Thêm node **Set** hoặc **HTTP Request** để lưu lịch sử hoạt động vào Google Sheets.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày và gửi báo cáo tổng hợp qua email.

4. **Tùy chỉnh cột trong Google Sheets**:
   - Nếu cần thêm cột mới, chỉ cần **thêm vào Google Sheet** và cập nhật trong các node `Get`/`Update`.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **xây dựng API REST CRUD chỉ trong 10 phút**, không cần viết code. **Hoàn toàn tự động hóa**, hoạt động 24/7, và dễ dàng mở rộng. **Hãy thử ngay và tiết kiệm thời gian phát triển backend!**

👉 **Bắt đầu ngay:** [Tải workflow từ n8n.io](https://n8n.io/workflows/8085) và import vào n8n của các sếp!