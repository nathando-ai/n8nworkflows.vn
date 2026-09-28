---
title: "🚀 Tự Động Hóa Thu Thập Dữ Liệu Form Web & Lưu Trữ Trên Google Sheets (Không Cần Code)"
description: "Workflow này tự động thu thập dữ liệu từ form web (POST request) và lưu trữ vào Google Sheets với tính năng sạch dữ liệu, thêm timestamp, và xử lý batch. Giúp doanh nghiệp tiết kiệm thời gian, giảm sai sót, và quản lý leads hiệu quả 24/7."
slug: "tieu-dong-hoa-thu-thap-du-lieu-form-web-luu-tren-google-sheets"
tags: [n8n, automation, lead-generation, google-sheets, no-code, webhook]
keywords: [n8n workflow tự động hóa, thu thập dữ liệu form web, lưu dữ liệu vào Google Sheets, tự động hóa CRM, giải pháp không code]
---

# 🚀 **Tự Động Hóa Thu Thập Dữ Liệu Form Web & Lưu Trữ Trên Google Sheets**

### **Giải pháp hoàn hảo cho doanh nghiệp cần tự động hóa thu thập leads, đăng ký, hoặc dữ liệu khách hàng mà không cần viết code!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên VPS để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập dữ liệu thủ công từ form vào Google Sheets.
- **Chính xác 100%**: Dữ liệu được tự động sạch sẽ và thêm timestamp tự động.
- **Hoạt động liên tục**: Thu thập dữ liệu 24/7, không phụ thuộc vào nhân viên.
- **Quản lý leads hiệu quả**: Dữ liệu được lưu trữ có cấu trúc, dễ dàng phân tích.
- **Thoát khỏi giới hạn code**: Sử dụng n8n để tự động hóa mà không cần viết một dòng code.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** và **Google Sheets OAuth2 API credentials** (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
2. **Một Google Sheet** đã được cấu hình với **các cột chính xác** (xem mẫu dưới đây).
3. **Một form web hoặc ứng dụng frontend** có thể gửi `POST` request đến webhook.
4. **Một instance n8n** (self-hosted hoặc cloud).
5. **API Key** của n8n để kết nối với Google Sheets.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **n8n Editor**.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc paste JSON).
3. Chọn **"Import"** để tải workflow vào.

:::note[Lưu ý]
- **Không thay đổi tên node** trừ khi cần thiết (để tránh lỗi trong quá trình chạy).
- **Không xóa node `Sticky Note`** (dùng để ghi chú, không ảnh hưởng đến logic).
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node Webhook (Triggers)**
- **Cấu hình**:
  - **HTTP Method**: `POST` (không thay đổi).
  - **Path**: `/93a81ced-e52c-4d31-96d2-c91a20bd7453` (có thể thay đổi để bảo mật).
- **Lưu ý**:
  - Form web phải gửi `POST` request đến URL này với **dữ liệu JSON** có cấu trúc:
    ```json
    {
      "business_name": "Tên Công Ty",
      "location": "Địa chỉ",
      "whatsapp": "Số Điện Thoại",
      "email": "Email",
      "name": "Tên Khách Hàng"
    }
    ```
  - **Không thay đổi tên field** trong JSON (nếu khác với node `Clean response data`).

#### **🔹 Node Code (Clean response data)**
- **Mục đích**: Sạch dữ liệu và thêm **timestamp** (`submitted_date`).
- **Lưu ý**:
  - **Không chỉnh sửa mã JavaScript** trong node này (nếu không biết code).
  - Nếu muốn thay đổi logic, các sếp có thể mở node và chỉnh sửa:
    ```javascript
    // Dữ liệu đầu vào từ Webhook
    const data = $input.all();

    // Sạch dữ liệu và thêm timestamp
    const cleanedData = {
      business_name: data.body.business_name.trim(),
      location: data.body.location.trim(),
      number: data.body.whatsapp.trim(),
      email: data.body.email.trim(),
      name: data.body.name.trim(),
      submitted_date: new Date().toISOString().split('T')[0] // YYYY-MM-DD
    };

    return cleanedData;
    ```
  - **Cấu trúc output phải khớp với cột trong Google Sheets**.

#### **🔹 Node Split In Batches (Loop Over Items)**
- **Mục đích**: Xử lý batch dữ liệu (nếu form gửi nhiều dữ liệu cùng lúc).
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu chỉ thu thập dữ liệu từ **một form** (mỗi lần submit là một request).
  - Nếu muốn **batching**, các sếp có thể cấu hình:
    - **Batch Size**: Số lượng item xử lý mỗi lần (ví dụ: 5).
    - **Thời gian chờ giữa batch**: Được điều khiển bởi node `Wait`.

#### **🔹 Node Google Sheets (Store Data in Sheet)**
- **Cấu hình bắt buộc**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Operation**: `append` (thêm dữ liệu mới vào cuối sheet).
  - **Document ID**: ID của Google Sheet (tìm trong URL sheet).
  - **Sheet Name**: Tên sheet (ví dụ: `Sheet1`).
  - **Column Mapping**:
    | Node Field       | Google Sheets Column       |
    |------------------|----------------------------|
    | `business_name`  | `Business Name`            |
    | `location`       | `Location`                 |
    | `number`         | `WhatsApp Number`          |
    | `email`          | `Email ` (có khoảng trắng sau) |
    | `name`           | `Name`                     |
    | `submitted_date` | `Date`                     |
- **Lưu ý**:
  - **Cột `Email ` trong Google Sheets phải có khoảng trắng sau** (không được xóa).
  - **Kiểm tra quyền**: Đảm bảo tài khoản OAuth2 có quyền **edit** sheet.

#### **🔹 Node Wait (Delay)**
- **Mục đích**: Tránh quá tải API Google Sheets khi xử lý batch.
- **Lưu ý**:
  - **Thời gian chờ**: 5 giây (có thể tăng lên nếu cần).
  - **Không cần chỉnh sửa** nếu chỉ xử lý đơn request.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một **dữ liệu mẫu** từ form web đến webhook.
   - Kiểm tra **output** của mỗi node để đảm bảo dữ liệu được sạch và lưu vào Google Sheets.
2. **Bật Active**:
   - Nhấp vào nút **"Active"** trên workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết nối với Slack/Telegram để thông báo**
- **Cách làm**:
  - Thêm node `Slack` hoặc `Telegram Bot` sau node `Google Sheets`.
  - Gửi thông báo khi dữ liệu được lưu thành công:
    ```json
    {
      "text": `📊 Dữ liệu mới được lưu vào Google Sheets!\nBusiness: $business_name\nEmail: $email`
    }
    ```

### **2. Lưu log vào Google Drive**
- **Cách làm**:
  - Thêm node `Google Drive` sau node `Google Sheets`.
  - Lưu file log (ví dụ: `submissions_${date}.csv`) để theo dõi lịch sử.

### **3. Gửi báo cáo định kỳ (hàng ngày/tuần)**
- **Cách làm**:
  - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày.
  - Thêm node `Email` (ví dụ: Gmail) để gửi báo cáo tổng hợp.

### **4. Tăng bảo mật webhook**
- **Cách làm**:
  - Thay đổi **path** của webhook (ví dụ: `/api/form-submit`).
  - Sử dụng **API Key** trong header của request:
    ```http
    POST /api/form-submit HTTP/1.1
    Content-Type: application/json
    Authorization: Bearer YOUR_API_KEY
    ```

---

## 📌 **Kết luận**
Workflow này giúp **tự động hóa thu thập dữ liệu từ form web** và lưu trữ vào Google Sheets **một cách nhanh chóng, chính xác và không cần code**. Đặc biệt phù hợp cho:
✅ **Doanh nghiệp cần thu thập leads** từ website.
✅ **Công ty cần đăng ký khách hàng** (spa, salon, dịch vụ).
✅ **Cá nhân muốn tự động hóa quản lý dữ liệu** mà không cần viết code.

**Hãy áp dụng ngay để tiết kiệm thời gian và giảm sai sót trong quản lý dữ liệu!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Join Cộng đồng n8n Việt Nam**: [Facebook Group](https://www.facebook.com/groups/n8nvietnam/)
- **Hỗ trợ kỹ thuật**: [n8n.io/support](https://n8n.io/support)