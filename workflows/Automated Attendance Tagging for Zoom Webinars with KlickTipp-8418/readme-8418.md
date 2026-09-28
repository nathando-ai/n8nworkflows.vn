---
title: "🎯 **Tự Động Hóa Gắn Thẻ Hiện Chỉnh Xem Trực Tuyến Zoom Cho Webinar Với KlickTipp (N8N)**"
description: "Workflow này tự động gắn thẻ cho người tham dự webinar Zoom dựa trên thời gian tham gia, giúp phân loại chính xác và tự động hóa chiến dịch tiếp thị theo hành vi thực tế. Giúp tiết kiệm thời gian, tăng hiệu quả phân khúc khách hàng và tối ưu hóa chiến dịch email/SMS."
slug: "tieu-dong-hoa-gan-the-hien-chinh-xem-truc-tuyen-zoom-klicktipp"
tags: [n8n, automation, zoom, klicktipp, marketing-automation, no-code, crm]
keywords: [n8n workflow zoom, tự động hóa webinar, gắn thẻ khách hàng, phân khúc khách hàng, marketing automation, klicktipp n8n, tự động hóa tiếp thị]

---

# **🚀 Tự Động Hóa Gắn Thẻ Hiện Chỉnh Xem Trực Tuyến Zoom Cho Webinar Với KlickTipp**

## **💡 Giới Thiệu: Tự Động Hóa Thay Thế Cho Công Việc Gắn Thẻ Manual Khó Khăn**
Các sếp đang tổ chức webinar thường gặp phải vấn đề **phân loại khách hàng theo thời gian tham gia** một cách thủ công, tốn thời gian và dễ sai sót. Hơn nữa, việc gửi email/SMS theo từng nhóm (đã tham gia đầy đủ, tham gia một phần, không tham gia) cũng phải làm bằng tay, làm giảm hiệu quả của chiến dịch tiếp thị.

**Workflow này giải quyết toàn bộ vấn đề đó bằng cách:**
✅ **Tự động nhận dữ liệu từ Zoom** khi webinar kết thúc.
✅ **Phân loại khách hàng** theo thời gian tham gia (đầy đủ ≥90%, một phần 60-89%, không tham gia).
✅ **Gắn thẻ tự động vào KlickTipp** để phân khúc khách hàng một cách chính xác.
✅ **Hỗ trợ nhiều loại webinar** (ví dụ: cho người mới vs. chuyên gia) trong một workflow duy nhất.
✅ **Tích hợp hoàn toàn với KlickTipp** (phù hợp GDPR) để gửi email/SMS tự động hóa sau webinar.

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gắn thẻ thủ công sau mỗi webinar.
- **Phân khúc chính xác**: Khách hàng được chia thành nhóm dựa trên hành vi thực tế (không phải giả định).
- **Chiến dịch cá nhân hóa**: Gửi email/SMS riêng biệt cho từng nhóm (ví dụ: khuyến mãi cho người tham gia đầy đủ, nhắc nhở cho người chưa tham gia).
- **Hoạt động 24/7**: Workflow chạy tự động ngay khi webinar kết thúc, không cần can thiệp của con người.
- **Dễ mở rộng**: Thêm nhiều webinar khác nhau mà không cần viết code.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Key**
- **Tài khoản Zoom** với quyền API:
  - **Scopes cần thiết**:
    - `webinar:read:webinar`
    - `webinar:read:list_past_participants`
    - `webinar:read:list_absentees`
  - **Webhook URL** từ n8n (sẽ được cấu hình sau).
- **Tài khoản KlickTipp** (đã tích hợp với n8n):
  - **API Key** của KlickTipp (được gọi là `klickTippApi` trong workflow).
  - **Các thẻ đã tạo sẵn** (xem phần **Cấu Hình KlickTipp** dưới đây).

#### **2. Cấu Hình Zoom**
- **Bật webhook cho sự kiện `webinar.ended`**:
  - Trong Zoom Admin Console → **Settings → Webhooks** → Thêm webhook mới với URL từ n8n (ví dụ: `https://your-n8n-instance/webhook/zoom`).
- **Tạo webinar mẫu** (nếu chưa có) để test:
  - Webinar cho người mới (ví dụ: *"Webinar Email Zustellung für Anfänger"*).
  - Webinar cho chuyên gia (ví dụ: *"Webinar Email Zustellung für Experten"*).

#### **3. Cấu Hình KlickTipp**
- **Tạo các trường tùy chỉnh (Custom Fields)** trong KlickTipp:
  | Tên Trường | Loại Dữ Liệu |
  |------------|--------------|
  | `Zoom | webinar selection` | Text |
  | `Zoom | webinar start` | Date & Time |
  | `Zoom | Join URL` | URL |
  | `Zoom | Registration ID` | Text |
  | `Zoom | Duration webinar` | Text |

- **Tạo các thẻ (Tags) cho phân khúc**:
  - **Cho webinar người mới**:
    - `Zoom webinar Email Zustellung für Anfänger`
    - `Zoom webinar Email Zustellung für Anfänger attended`
    - `Zoom webinar Email Zustellung für Anfänger attended fully`
    - `Zoom webinar Email Zustellung für Anfänger not attended`
  - **Cho webinar chuyên gia**:
    - `Zoom webinar Email Zustellung für Experten`
    - `Zoom webinar Email Zustellung für Experten attended`
    - `Zoom webinar Email Zustellung für Experten attended fully`
    - `Zoom webinar Email Zustellung für Experten not attended`

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/8418](https://n8n.io/workflows/8418) (chọn **Export as JSON**).
  2. Trong n8n Editor → **Import** → Chọn file JSON vừa tải.
  3. Chọn **Import** để thêm workflow vào canvas.

- **Cách 2: Copy/Paste JSON**
  1. Copy toàn bộ mã JSON từ [n8n.io/workflows/8418](https://n8n.io/workflows/8418).
  2. Trong n8n Editor → **Import** → Chọn **Paste JSON** và dán mã.
  3. Chọn **Import** để thêm workflow.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **25 node**, nhưng chỉ cần chú ý đến các node quan trọng sau:

##### **A. Cấu Hình Webhook Zoom (Node: "Listen to ending Zoom webinars")**
- **Tham số cần điền**:
  - **Path**: `zoom` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Credentials**: Chọn `zoomOAuth2Api` (sẽ cấu hình sau).
  - **Validation**:
    - Node **"URL Validation check"** sẽ kiểm tra HMAC của Zoom. **Không cần chỉnh** nếu đã cấu hình webhook đúng trong Zoom.

##### **B. Cấu Hình API Zoom (Nodes: "Get past Zoom webinar participants" & "Get past Zoom webinar absentees")**
- **Credentials**: Chọn `zoomOAuth2Api` (tạo mới trong n8n):
  1. Trong n8n → **Credentials** → **Add** → Chọn **Zoom OAuth2**.
  2. Điền:
     - **Client ID** & **Client Secret** từ Zoom Developer Console.
     - **Refresh Token** (lấy từ OAuth2 Flow của Zoom).
  3. **Tham số HTTP Request**:
     - **Method**: `GET`.
     - **URL**: `https://api.zoom.us/v2/webinars/{webinar_id}/participants` (cho danh sách tham dự) và `https://api.zoom.us/v2/webinars/{webinar_id}/absentees` (cho danh sách vắng mặt).
     - **Headers**:
       - `Authorization: Bearer {access_token}` (tự động sinh bởi OAuth2).
       - `Content-Type: application/json`.

##### **C. Cấu Hình KlickTipp (Nodes: "Tag participant for full attendance", "Tag participant for general attendance", "Tag absentee for non attendance")**
- **Credentials**: Chọn `klickTippApi` (tạo mới trong n8n):
  1. Trong n8n → **Credentials** → **Add** → Chọn **KlickTipp**.
  2. Điền:
     - **API Key** từ tài khoản KlickTipp.
     - **Base URL** (nếu khác mặc định, ví dụ: `https://api.klicktipp.com`).
- **Tham số Tagging**:
  - **Resource**: `contact-tagging` (không thay đổi).
  - **Contact ID**: Sẽ tự động lấy từ dữ liệu Zoom.
  - **Tags**: Workflow sẽ gắn thẻ tự động dựa trên thời gian tham gia (xem phần **Logic Phân Loại** dưới đây).

##### **D. Logic Phân Loại (Nodes: "Check full attendance", "Check general attendance", "Route by meeting name")**
- **Cách hoạt động**:
  1. **Node "Check full attendance"**:
     - Kiểm tra nếu thời gian tham gia ≥ 90% → Gắn thẻ `attended fully`.
  2. **Node "Check general attendance"**:
     - Kiểm tra nếu thời gian tham gia ≥ 60% → Gắn thẻ `attended`.
  3. **Node "Route by meeting name"**:
     - Chuyển hướng dữ liệu theo tên webinar (ví dụ: "Anfänger" vs. "Experten") để gắn thẻ chính xác.

##### **E. Lọc Người Nội Bộ (Node: "Filter internal users")**
- **Cách cấu hình**:
  - Thêm điều kiện lọc (ví dụ: loại bỏ email `@company.com`).
  - **Tham số**:
    - **Expression**: `{{$json["email"].toLowerCase()}} !== "internal@example.com"`.

##### **F. Thời Gian Chờ (Node: "Wait 1 second")**
- **Lý do**: Zoom API có giới hạn request, node này giúp tránh bị block.
- **Không cần chỉnh** (mặc định 1 giây).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu**:
   - Chọn **Run Workflow** và chọn **Test Execution**.
   - Chọn **Zoom Webinar Data** (nếu có mẫu) hoặc tạo một webinar test.
   - Kiểm tra:
     - Webhook có nhận được không?
     - Dữ liệu tham dự/không tham dự có được lấy không?
     - Thẻ trong KlickTipp có được gắn đúng không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
- **Thêm Slack/Telegram Notifications**:
  - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi webinar kết thúc và gắn thẻ thành công.
  - Ví dụ: *"Webinar 'Email Zustellung für Anfänger' kết thúc! Đã gắn thẻ cho 50 người tham gia."*

- **Lưu Log Dữ Liệu**:
  - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử webinar, danh sách tham dự và thẻ đã gắn.
  - Cách cấu hình:
    ```json
    {
      "name": "Log Webinar Data",
      "type": "googleSheets",
      "credentials": ["googleSheetsApi"],
      "keyParameters": {
        "sheetName": "Zoom Webinar Logs",
        "range": "Sheet1!A1"
      }
    }
    ```

- **Gửi Báo Cáo Định Kỳ**:
  - Sử dụng node **KlickTipp Email Campaign** để gửi báo cáo tổng hợp cho team marketing hàng tuần.
  - Ví dụ: *"Tổng kết webinar tuần qua: 120 người tham gia, 30% đã tham gia đầy đủ."*

- **Tích Hợp với CRM Khác**:
  - Nếu sử dụng HubSpot, Salesforce, hoặc Mailchimp, có thể thay thế KlickTipp bằng node tương ứng (ví dụ: `hubspot` hoặc `mailchimp`).
  - Cách thay đổi:
    - Thay node `CUSTOM.klicktipp` bằng `hubspot` và cấu hình lại API key.

- **Cập Nhật Ngưỡng Tham Gia**:
  - Nếu muốn thay đổi ngưỡng (ví dụ: từ 90% → 80% để gắn thẻ "đầy đủ"), chỉnh node **"Check full attendance"** như sau:
    ```json
    {
      "name": "Check full attendance",
      "type": "if",
      "expression": "{{$json.duration}} >= 0.8"  // Thay 0.9 thành 0.8
    }
    ```

---

### **📌 Kết Luận: Áp Dụng Ngay Để Tăng Hiệu Quả Chiến Dịch!**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc gắn thẻ thủ công, đồng thời **tăng độ chính xác** của phân khúc khách hàng. Bằng cách tự động hóa quá trình này, các sếp có thể:
✔ **Tăng tỷ lệ chuyển đổi** với email/SMS cá nhân hóa.
✔ **Tối ưu hóa ngân sách marketing** bằng cách chỉ gửi cho nhóm mục tiêu.
✔ **Mở rộng quy mô** dễ dàng với nhiều webinar khác nhau.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test với webinar mẫu** và bắt đầu tự động hóa!

**Chia sẻ kết quả** của các sếp sau khi áp dụng để cùng học hỏi nhé! 🚀