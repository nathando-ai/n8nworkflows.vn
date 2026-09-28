---
title: "🚀 Tự Động Hóa Đồng Bộ Hàng Hóa Từ Google Sheets Sang Odoo Với Tải Ảnh Tự Động – Giảm Thời Gian Làm Việc 90%!"
description: "Workflow này tự động đồng bộ hóa hàng hóa từ Google Sheets sang Odoo, bao gồm kiểm tra mã vạch, tải ảnh từ URL, và cập nhật trạng thái hoàn tất. Giúp các sếp tiết kiệm thời gian và tránh sai sót khi nhập liệu thủ công."
slug: "tieu-dong-bo-hang-hoa-tu-google-sheets-sang-odoo"
tags: [n8n, automation, odoo, google-sheets, crm, no-code]
keywords: [tự động hóa odoo, đồng bộ hàng hóa google sheets, tải ảnh tự động, workflow n8n, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Đồng Bộ Hàng Hóa Từ Google Sheets Sang Odoo Với Tải Ảnh Tự Động**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Nhập liệu hàng hóa** từ Google Sheets sang Odoo một cách thủ công, tốn thời gian và dễ sai sót.
- **Kiểm tra trùng lặp** sản phẩm bằng mã vạch, gây ra rủi ro mất dữ liệu hoặc trùng lặp.
- **Tải ảnh sản phẩm** từ URL lên Odoo, phải làm thủ công, mất thời gian và không đồng bộ.
- **Cập nhật trạng thái** sau khi đồng bộ, phải quay lại Google Sheets để đánh dấu "Hoàn tất".

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình chỉ với một dòng dữ liệu mới trên Google Sheets!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Đồng bộ hàng trăm sản phẩm chỉ trong vài giây thay vì nhiều giờ.
✅ **Tránh sai sót**: Kiểm tra trùng lặp tự động bằng mã vạch, không còn nhập nhầm dữ liệu.
✅ **Tải ảnh tự động**: Nếu URL ảnh được cung cấp, hệ thống sẽ tự tải và gắn vào sản phẩm Odoo.
✅ **Cập nhật trạng thái tự động**: Sau khi đồng bộ thành công, Google Sheets sẽ tự động đánh dấu "Hoàn tất".
✅ **Hoàn toàn tự động hóa**: Không cần can thiệp thủ công, hoạt động 24/7.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets với các cột: **Mã vạch (Barcode)**, **Tên sản phẩm (Name)**, **Mô tả (Description)**, **URL ảnh (Image URL)**, **Danh mục (Category ID)**.
   - **Cột trạng thái (Status)** để lưu trạng thái đồng bộ (ví dụ: "Chờ đồng bộ", "Đã hoàn tất").
   - **Mã API Google Sheets** (tạo từ [Google Cloud Console](https://console.cloud.google.com/)).

2. **Tài khoản Odoo**:
   - **URL Odoo** (ví dụ: `https://tên_odoo.com`).
   - **Database Name**, **Username**, **Password** (để kết nối API).
   - **API Key** (tạo từ **Settings > Technical > API** trong Odoo).

3. **Hệ thống n8n**:
   - Cài đặt n8n trên **VPS riêng** (Self-hosted) để workflow hoạt động 24/7.
   - Cài đặt **n8n-nodes-base** và **n8n-nodes-odoo** (nếu chưa có).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **Workflow Editor**.
2. Nhấp vào **Import** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/14928)).
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14928) và paste vào **Import from JSON** trong Editor.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Cấu Hình Google Sheets Trigger**
- **Node: "On New Row in Sheets"**
  - **Google Sheets Credentials**: Chọn credential đã tạo từ **Google Cloud Console**.
  - **Sheet Name**: Điền tên bảng Google Sheets chứa dữ liệu sản phẩm.
  - **Range**: Điền phạm vi dữ liệu (ví dụ: `Sheet1!A:Z`).
  - **Trigger on Row Update**: Bật **ON** để workflow kích hoạt khi có dòng mới hoặc cập nhật.

#### **🔹 Cấu Hình Odoo API**
- **Node: "Check Odoo for Barcode"**, **"Get Odoo Category"**, **"Create Product (With Image)"**, **"Create Product (No Image)"**
  - **Credentials**: Chọn credential **odooApi** (tạo từ **Settings > Technical > API** trong Odoo).
  - **URL**: Điền URL Odoo (ví dụ: `https://tên_odoo.com`).
  - **Database Name**, **Username**, **Password**: Điền thông tin kết nối Odoo.
  - **Resource**:
    - **"Check Odoo for Barcode"**: Đặt `resource: product.template` (mã vạch là `default_code`).
    - **"Get Odoo Category"**: Đặt `resource: product.category`.
    - **"Create Product (With Image)" & "Create Product (No Image)"**: Đặt `resource: product.template`.

#### **🔹 Cấu Hình Cập Nhật Trạng Thái**
- **Node: "Mark as Done in Sheet"**
  - **Google Sheets Credentials**: Chọn credential Google Sheets tương tự như trước.
  - **Range**: Điền phạm vi cột trạng thái (ví dụ: `Sheet1!E:E`).
  - **Value**: Đặt giá trị cập nhật thành **"Done"** (hoặc tùy chỉnh theo yêu cầu).

#### **🔹 Cấu Hình Tải Ảnh (Nếu Có URL)**
- **Node: "Download Image"**
  - **URL**: Điền vào `{{$json["Image URL"]}}` (hoặc cột tương ứng trong Google Sheets).
  - **Headers**: Thêm `Accept: image/*` để đảm bảo tải đúng định dạng ảnh.

- **Node: "Convert Image to Base64"**
  - **Operation**: Chọn `binaryToPropery`.
  - **Property**: Đặt `image_base64` (hoặc tên biến tùy chỉnh).

#### **🔹 Cấu Hình Xử Lý Lỗi**
- **Node: "Wait on Error"**
  - **Time**: Đặt **1 phút** để retry nếu có lỗi (ví dụ: Google Sheets update thất bại).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một dòng mẫu:
   - Thêm một dòng mới vào Google Sheets với dữ liệu mẫu (ví dụ: Mã vạch `ABC123`, Tên `Sản phẩm mẫu`, URL ảnh `https://example.com/image.jpg`).
   - Chạy **Test Run** trong n8n để kiểm tra workflow.
2. **Bật Active**:
   - Sau khi test thành công, nhấp **Active** để workflow chạy tự động khi có dòng mới.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Hợp Với Slack/Telegram**
- Thêm **Node Slack/Telegram** sau **"Mark as Done in Sheet"** để thông báo khi đồng bộ thành công/lỗi.
- Ví dụ:
  ```json
  {
    "name": "Notify Slack",
    "type": "slackWebhook",
    "credentials": ["slackWebhook"],
    "keyParameters": {
      "text": "🚀 Đồng bộ sản phẩm {{$json["Name"]}} thành công!"
    }
  }
  ```

### **🔹 Lưu Log Lỗi**
- Thêm **Node StickyNote** để ghi log lỗi:
  ```json
  {
    "name": "Log Error",
    "type": "stickyNote",
    "keyParameters": {
      "text": "Lỗi đồng bộ: {{$json["error"]}}"
    }
  }
  ```

### **🔹 Gửi Báo Cáo Định Kỳ**
- Sử dụng **Node Set** + **Node Schedule** để gửi báo cáo hàng ngày về số lượng sản phẩm đồng bộ thành công.

### **🔹 Tùy Chỉnh Cấu Hình Odoo**
- Nếu Odoo có cấu trúc khác (ví dụ: sử dụng `product.product` thay vì `product.template`), cập nhật `resource` trong các node Odoo tương ứng.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập liệu thủ công, đồng thời **tránh sai sót** và **tăng hiệu suất** cho hệ thống Odoo. Với chỉ một dòng dữ liệu mới trên Google Sheets, hệ thống sẽ tự động:
✔ Kiểm tra trùng lặp bằng mã vạch.
✔ Tải ảnh từ URL (nếu có).
✔ Tạo sản phẩm trong Odoo.
✔ Cập nhật trạng thái "Hoàn tất".

**🚀 Hãy áp dụng ngay workflow này và tự động hóa quy trình bán hàng của mình!**

---
**💡 Cần hỗ trợ thêm?**
- Trả lời câu hỏi trong [n8n Community](https://community.n8n.io/).
- Liên hệ tác giả [Khaled Yasser](https://n8n.io/workflows/14928) để tùy chỉnh workflow theo nhu cầu cụ thể.