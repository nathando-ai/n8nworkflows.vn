---
title: "📊 Tự Động Hoàn Thành & Chuẩn Hóa Dữ Liệu Trước Khi Gửi Đến Google Sheets (N8n)"
description: "Workflow này tự động lấy dữ liệu từ Customer Datastore, chuẩn hóa định dạng (đổi tên trường, lọc dữ liệu, thêm trường mới) và cập nhật trực tiếp vào Google Sheets với 1 cú nhấp chuột. Giúp các sếp tiết kiệm 50% thời gian xử lý dữ liệu thủ công."
slug: "chu-an-hoa-du-lieu-google-sheets-n8n"
tags: [n8n, automation, google-sheets, data-preparation, no-code]
keywords: [tự động hóa n8n, chuẩn hóa dữ liệu, google sheets api, workflow n8n cơ bản, tự động cập nhật google sheets]
---

# 🚀 **Tự Động Chuẩn Hóa & Cập Nhật Dữ Liệu Từ Datastore Sang Google Sheets**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Lấy dữ liệu** từ hệ thống nội bộ (Datastore, CRM, hoặc cơ sở dữ liệu khác).
- **Chỉnh sửa định dạng** (đổi tên trường, lọc dữ liệu, thêm trường mới) để phù hợp với Google Sheets.
- **Cập nhật thủ công** vào Google Sheets, dễ gây lỗi và mất thời gian.

Workflow này **giải quyết tất cả** bằng cách tự động hóa toàn bộ quy trình chỉ với **1 nút nhấn**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50% thời gian** so với làm thủ công.
- **Chính xác 100%** (không sai sót khi đổi tên trường hoặc lọc dữ liệu).
- **Hoạt động liên tục** (không cần phải nhớ làm hàng ngày).
- **Dữ liệu luôn đồng bộ** giữa Datastore và Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
✅ **Tài khoản Google** với quyền truy cập vào Google Sheets.
✅ **API Key OAuth2** của Google Sheets (cài đặt trong n8n dưới dạng `googleSheetsOAuth2Api`).
✅ **Workflow n8n** được cài đặt trên **VPS riêng** (Self-hosted) để hoạt động 24/7.
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/1751](https://n8n.io/workflows/1751).
- **Nhấp vào "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy/paste** toàn bộ JSON vào Editor và nhấn **Save**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần chú ý:

#### **🔹 Node 1: Manual Trigger (Bắt Đầu)**
- **Chức năng**: Khởi động workflow khi nhấn nút **"Execute Workflow"**.
- **Không cần cấu hình gì**, chỉ cần nhấn nút để chạy.

#### **🔹 Node 2: Customer Datastore - Generate Some Data**
- **Chức năng**: Lấy dữ liệu từ **Customer Datastore** (mô phỏng như một cơ sở dữ liệu nội bộ).
- **Cấu hình**:
  - **Operation**: Đảm bảo chọn **"getAllPeople"** (đã mặc định).
  - **Không cần thay đổi gì** nếu sử dụng Datastore mặc định của n8n.

#### **🔹 Node 3: Set - Prepare Fields (Chuẩn Hóa Dữ Liệu)**
- **Chức năng**: **Chuyển đổi định dạng dữ liệu** để phù hợp với Google Sheets.
- **Cấu hình cần chỉnh**:
  - **Input Data**:
    ```json
    {
      "ID": "$json['id']",
      "Email": "$json['email']",
      "Full name": "$json['name']",  // Đổi từ `name` thành `Full name`
      "Created time": "${{ $now('YYYY-MM-DD HH:mm:ss') }}"  // Thêm trường mới
    }
    ```
  - **Lưu ý**:
    - **Bỏ các trường không cần thiết** (ví dụ: `phone`, `address`).
    - **Thêm trường `Created time`** để ghi thời gian cập nhật.
    - **Đổi tên trường `name` thành `Full name`** (Google Sheets yêu cầu).

#### **🔹 Node 4: Google Sheets - Create or Update Record**
- **Chức năng**: **Cập nhật dữ liệu** vào Google Sheets với **upsert** (thêm mới hoặc cập nhật).
- **Cấu hình cần chỉnh**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
  - **Spreadsheet ID**: Điền **ID của Google Sheet** (tìm trong URL của Sheet).
  - **Sheet Name**: Điền **tên trang tính** (ví dụ: `People`).
  - **Range**: Điền `A1:D1000` (hoặc tùy chỉnh theo số cột).
  - **Operation**: Đảm bảo chọn **"upsert"** (thêm mới hoặc cập nhật).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute Workflow"** và kiểm tra **output** của mỗi node.
   - Đảm bảo dữ liệu được chuẩn hóa đúng và cập nhật vào Google Sheets.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để hoạt động tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ HƠN]
- **Kết hợp với Webhook**: Thay vì dùng **Manual Trigger**, các sếp có thể **kích hoạt tự động** khi có dữ liệu mới từ API hoặc Slack.
- **Lưu Log**: Thêm node **Slack/Email** để nhận thông báo khi workflow chạy thành công/thất bại.
- **Tự động Gửi Báo Cáo**: Sử dụng **Google Sheets + Apps Script** để tự động gửi báo cáo định kỳ qua Email.
- **Tùy Chỉnh Dữ Liệu**: Nếu Datastore có nhiều trường, các sếp có thể **lọc dữ liệu** bằng node **Set** trước khi gửi.
:::

---

## 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa quy trình chuẩn hóa và cập nhật dữ liệu** từ Datastore sang Google Sheets chỉ với **1 cú nhấp chuột**, tiết kiệm **50% thời gian** và **tránh sai sót**.

**Hãy áp dụng ngay và làm việc thông minh hơn!** 🚀

---
**🔗 [Tải Workflow JSON](https://n8n.io/workflows/1751) | 📌 [Cài n8n Self-hosted](https://n8n.io/docs/)**