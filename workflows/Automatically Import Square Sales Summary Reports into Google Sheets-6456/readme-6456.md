---
title: "📊 Tự Động Nhập Báo Cáo Doanh Thu Square Vào Google Sheets - Giảm 90% Thời Gian Lập Báo Cáo"
description: "Workflow tự động hóa 100% không code kết nối Square API với Google Sheets để lấy báo cáo doanh thu hàng ngày cho tất cả cửa hàng, giúp các sếp tiết kiệm thời gian và phân tích dữ liệu chính xác hơn."
slug: "tieu-dong-nhap-bao-cao-square-vao-google-sheets"
tags: [n8n, automation, square-api, google-sheets, crm, no-code]
keywords: [tự động hóa square, báo cáo doanh thu tự động, google sheets automation, square api integration, workflow n8n]
---

# 🚀 **Tự Động Nhập Báo Cáo Doanh Thu Square Vào Google Sheets - Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- Tải báo cáo doanh thu từ **Square Dashboard** (trang **Reports > Sales Summary**).
- Chuyển dữ liệu thủ công vào **Google Sheets** hoặc Excel.
- Sửa chữa lỗi nhập liệu, so sánh dữ liệu giữa các cửa hàng.
- Tạo báo cáo định kỳ cho bộ phận tài chính, marketing hoặc quản lý.

**Kết quả?** Dữ liệu không đồng bộ, mất thời gian, và khó theo dõi xu hướng doanh thu dài hạn.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** lập báo cáo hàng ngày.
- **Dữ liệu chính xác 100%** (không sai sót nhập liệu).
- **Tự động cập nhật hàng ngày** (không cần làm thủ công).
- **Dễ dàng phân tích** với Google Sheets (biểu đồ, lọc dữ liệu, báo cáo tự động).
- **Kết nối với nhiều công cụ** (Slack, Email, CRM) để báo cáo tự động.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Square API Key** (Header Auth):
   - Tạo tại [Square Developer Dashboard](https://developer.squareup.com/dashboard/).
   - Cấu hình trong n8n với **Header Auth** (Name: `Authorization`, Value: `Bearer <API_KEY>`).
2. **Google Sheets OAuth2 Credential**:
   - Tạo trong n8n với quyền **Edit** trên Google Sheet.
3. **Google Sheet đã chuẩn bị sẵn** với các cột:
   ```
   | Date       | Location ID | Location Name | Gross Sales | Discounts | Returns | Net Sales | Taxes | Tips | Cash Rounding | Total Money Collected | Cash | Card | Gift Card | Other Payment Method | Fees | Net Total |
   ```
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6456) hoặc copy/paste JSON từ trang này.
- Vào **n8n Editor** → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Node "Schedule Trigger" (Đặt lịch chạy)**
- **Thời gian chạy mặc định**: 4:00 AM hàng ngày (lấy dữ liệu ngày hôm trước).
- **Lưu ý**:
  - Đảm bảo **n8n chạy 24/7** (self-hosted trên VPS).
  - Nếu muốn chạy vào giờ khác, chỉnh `cron` trong node này (ví dụ: `0 0 8 * * ?` để chạy 8:00 AM).

##### **B. Node "Get Square Locations" (Lấy danh sách cửa hàng)**
- **Credentials**: Chọn **Header Auth** đã tạo trước (Square API Key).
- **URL**: Sử dụng API mặc định của Square:
  ```http
  https://connect.squareup.com/v2/locations
  ```
- **Headers**:
  ```json
  {
    "Authorization": "Bearer YOUR_SQUARE_API_KEY",
    "Content-Type": "application/json"
  }
  ```

##### **C. Node "Get Sales from Square" (Lấy dữ liệu doanh thu)**
- **Credentials**: Giống node trước (Square API Key).
- **URL**: Sử dụng API Square Orders:
  ```http
  https://connect.squareup.com/v2/locations/{location_id}/transactions
  ```
  - Tham số động (`{location_id}`) sẽ được lấy từ node trước.
- **Query Parameters**:
  ```json
  {
    "date": "YYYY-MM-DD",  // Ngày hôm trước (được tính tự động)
    "limit": 1000,         // Giá trị mặc định (có thể tăng nếu cần)
    "order_by": "created_at",
    "sort_order": "desc"
  }
  ```

##### **D. Node "Compile Sales Reports" (Tính tổng hợp báo cáo)**
- **Code Node**: Dùng mã JavaScript để tính toán các chỉ số như:
  - **Gross Sales**, **Net Sales**, **Taxes**, **Tips**, **Fees**, v.v.
- **Lưu ý**:
  - Đảm bảo **công thức tính toán chính xác** như Square Dashboard.
  - Ví dụ mã mẫu (có thể chỉnh sửa):
    ```javascript
    // Tính tổng Gross Sales
    const grossSales = items.reduce((sum, item) => sum + item.amount_money.amount, 0);

    // Tính Net Sales (Gross - Discounts - Returns)
    const netSales = grossSales - discounts - returns;

    return {
      ...item,
      GrossSales: grossSales,
      NetSales: netSales,
      // ... các chỉ số khác
    };
    ```

##### **E. Node "Upload Sales to Google Sheets" (Nhập vào Google Sheets)**
- **Credentials**: Chọn **Google Sheets OAuth2** đã tạo.
- **Spreadsheet ID**: ID của Google Sheet (tìm trong URL: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`).
- **Sheet Name**: Tên tab trong Google Sheet (ví dụ: `DoanhThuHangNgay`).
- **Range**: `A1` (để thêm dữ liệu từ hàng 1).
- **Operation**: `append` (thêm dữ liệu mới vào cuối).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn node **Schedule Trigger** → Nhấn **Run Workflow**.
   - Kiểm tra kết quả trong Google Sheet.
2. **Bật Active**:
   - Đánh dấu workflow thành **Active** để chạy tự động hàng ngày.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo qua Email/Slack**:
   - Kết nối với **n8n-nodes-base.email** hoặc **n8n-nodes-base.slack** để gửi báo cáo tự động.
2. **Lưu log dữ liệu**:
   - Sử dụng **n8n-nodes-base.file** để lưu lịch sử báo cáo vào Google Drive.
3. **Tính toán chi tiết hơn**:
   - Thêm node **Code** để tính **tỷ lệ doanh thu theo cửa hàng**, **trung bình hàng ngày**, hoặc **so sánh với tháng trước**.
4. **Chỉnh sửa thời gian chạy**:
   - Đặt lịch chạy **tối đa 2 lần/ngày** (ví dụ: 4:00 AM và 4:00 PM) nếu cần dữ liệu thời gian thực.
5. **Kết nối với CRM**:
   - Sử dụng dữ liệu doanh thu để cập nhật **CRM** (HubSpot, Zoho) hoặc tính **commission cho nhân viên**.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập liệu thủ công, đồng thời **cung cấp dữ liệu chính xác** để phân tích và báo cáo hiệu quả. **Chỉ cần 10 phút setup**, các sếp sẽ có **báo cáo doanh thu tự động hóa 100%** hàng ngày!

**Hành động ngay**:
1. **Cài n8n trên VPS** (self-hosted) để workflow chạy 24/7.
2. **Import workflow** và cấu hình Square API + Google Sheets.
3. **Bật Active** và theo dõi kết quả!

---
:::note[💡 Gợi Ý Hạ Tầng]
Để workflow chạy ổn định, các sếp nên **self-host n8n trên VPS** với cấu hình tối thiểu:
- **RAM**: 2GB+
- **CPU**: 1 vCore
- **Đisk**: 20GB SSD

👉 **Đăng ký VPS TinoHost** (mã giảm giá **VPSN8N** - giảm tới 39%):
[https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)

👉 **Đăng ký VPS Xeon 4GB chỉ 50k/tháng**:
[https://my.bnix.one/aff.php?aff=172](https://my.bnix.one/aff.php?aff=172)
:::