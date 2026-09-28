---
title: "🚀 Tự Động Hóa Kiểm Tra & Đánh Giá AI Email Bulk với ZeroBounce (Không Cần Code)"
description: "Workflow tự động hóa kiểm tra tính hợp lệ và đánh giá AI email bulk với ZeroBounce, giúp các sếp loại bỏ email không hợp lệ, tối ưu hóa tỷ lệ giao nhận và bảo vệ danh tiếng gửi email. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-kiem-tra-danh-gia-email-zero-bounce"
tags: [n8n, automation, no-code, zero-bounce, email-marketing, lead-generation]
keywords: [tự động hóa email, kiểm tra email hợp lệ, ZeroBounce n8n, đánh giá AI email, tự động hóa marketing, bulk email validation]
---

# 🚀 **Tự Động Hóa Kiểm Tra & Đánh Giá AI Email Bulk với ZeroBounce (Không Cần Code)**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Gửi email bulk nhưng **tỷ lệ rebounce (email không hợp lệ) cao**, **tốn thời gian kiểm tra từng địa chỉ**, và **rủi ro danh tiếng gửi email bị ảnh hưởng**? Các sếp đang mất **từ 5-10 giờ/tuần** để:
- Kiểm tra tính hợp lệ của email thủ công (hoặc bằng các công cụ có giới hạn).
- Loại bỏ email spam trap, disposable, hoặc không tồn tại.
- Đánh giá độ tin cậy của mỗi địa chỉ để tối ưu hóa chiến dịch.

**ZeroBounce** là giải pháp **99.6% chính xác** với API nhanh chóng, nhưng phải tự động hóa để **tiết kiệm thời gian và giảm thiểu lỗi**. Workflow này **giải quyết tất cả** với **không cần viết một dòng code nào!**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Loại bỏ 99.6% email không hợp lệ** (spam trap, disposable, fake).
✅ **Đánh giá AI độ tin cậy** (score 0-10) để phân loại email thành **High/Medium/Low Risk**.
✅ **Hoạt động 24/7** trên VPS, không cần can thiệp thủ công.
✅ **Bảo vệ danh tiếng gửi email** bằng cách loại bỏ email có nguy cơ rebounce cao.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản ZeroBounce**
- **API Key** của ZeroBounce (miễn phí 100 credit để test).
  👉 [Tạo API Key tại đây](https://www.zerobounce.net/members/API)
- **Tài khoản Premium** (nếu muốn sử dụng full tính năng).

### **2. File Email Bulk (CSV/Excel)**
- File chứa **danh sách email** (cột `email`) và **tùy chọn IP** (nếu cần).
- **Dữ liệu mẫu** có thể là:
  ```csv
  email,ip
  test@example.com,123.123.123.123
  fake@mailinator.com,456.456.456.456
  ```

### **3. Hệ Thống n8n**
- **Self-hosted n8n** trên VPS (để workflow chạy 24/7).
  :::info[Gợi ý hạ tầng cho n8n]
  Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
  :::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11538](https://n8n.io/workflows/11538).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn file JSON** đã tải và nhấn **"Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo **workflow mới**.
2. **Nhấn "Import"** → **"Paste JSON"**.
3. **Dán JSON** từ [tại đây](https://github.com/n8n-io/workflows/blob/master/workflows/11538.json) và nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 Cấu Hình ZeroBounce API**
1. **Tạo Credential ZeroBounce**:
   - Trong n8n Editor, nhấn **"Credentials"** → **"Add"** → **"ZeroBounce"**.
   - Điền:
     - **API Key**: Từ ZeroBounce (tạo ở bước trên).
     - **Base URL**: `https://api.zerobounce.net/v2`.
     - **Sandbox Mode**: **Bật** (để test với email giả).

2. **Cấu Hình Node "Send file for validation"**:
   - **File Input**: Chọn **`Sandbox emails`** (node `set`).
   - **Format**: `csv`.
   - **Headers**: `email,ip` (nếu có IP).

3. **Cấu Hình Node "Send file for scoring"**:
   - **File Input**: **Kết nối với output của node "Send file for validation"**.
   - **Resource**: `scoring`.

#### **🔹 Cấu Hình File Input (Sandbox Emails)**
- **Nếu test**: Sử dụng **email sandbox** (miễn phí, không tốn credit).
  Ví dụ:
  ```csv
  email,ip
  test1@zerobounce.net,
  test2@zerobounce.net,
  ```
- **Nếu sản xuất**: Thay bằng **file email thực tế** của doanh nghiệp.

#### **🔹 Cấu Hình Switch Nodes (Lọc Kết Quả)**
- **Node "Is valid?"**:
  - **Case 1**: `valid` → Đi đến **"High/Medium/Low score"**.
  - **Case 2**: `invalid` → Đi đến **"Not valid"**.
- **Node "Filter by score"**:
  - **High Score (8-10)**: Email **an toàn** để gửi.
  - **Medium Score (5-7)**: Email **cần theo dõi**.
  - **Low Score (0-4)**: Email **rủi ro cao**, nên loại bỏ.

#### **🔹 Thời Gian Chờ (Wait Nodes)**
- **Thời gian mặc định**: 5 phút (để ZeroBounce xử lý).
- **Nếu quá lâu**: Workflow sẽ **dừng và báo lỗi** (`Bulk validation failed`/`Bulk scoring failed`).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ liệu Mẫu**:
   - Nhấn **"Execute workflow"** và chọn **file test**.
   - Kiểm tra kết quả trong **node "Validation results"**.

2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật "Active"** để workflow chạy tự động.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối với Slack/Telegram**
- **Thêm node Slack/Telegram** sau **"High Score"** để thông báo email **sẵn sàng gửi**.
- **Cấu hình**:
  ```json
  {
    "webhookUrl": "https://hooks.slack.com/services/...",
    "message": "🚀 Email {{$node["Validation results"].json["email"]}} đã được xác nhận và có score cao!"
  }
  ```

### **2. Lưu Log vào Google Sheets/Notion**
- **Thêm node Google Sheets** sau **"Medium/Low Score"** để ghi log email **rủi ro**.
- **Cấu hình**:
  - **Sheet Name**: `Email_Risk_Log`.
  - **Columns**: `Email`, `Score`, `Status`, `Date`.

### **3. Gửi Báo Cáo Định Kỳ**
- **Sử dụng node `set` + `email`** để gửi báo cáo tuần/month về:
  - **Tỷ lệ email hợp lệ**.
  - **Số email bị loại bỏ**.
  - **Trend score trung bình**.

### **4. Tích Hợp với CRM (HubSpot, Salesforce)**
- **Sau khi lọc email High Score**, gửi dữ liệu vào **HubSpot/Salesforce** để **nâng cấp lead**.
- **Cấu hình**:
  - Node **HubSpot API** → **Create Contact** với email đã xác nhận.

---
## **📌 Kết Luận**
Workflow này **giải quyết toàn bộ vấn đề rebounce email** bằng cách:
✔ **Kiểm tra 99.6% email hợp lệ** với ZeroBounce.
✔ **Đánh giá AI độ tin cậy** (score 0-10).
✔ **Phân loại email** thành **High/Medium/Low Risk**.
✔ **Hoạt động tự động 24/7** trên VPS.

**Hành động ngay!**
1. **Import workflow** và cấu hình ZeroBounce API.
2. **Test với file email mẫu**.
3. **Bật Active** và **tự động hóa email marketing** của doanh nghiệp!

👉 [Tải workflow ngay](https://n8n.io/workflows/11538) và **tiết kiệm thời gian, tăng tỷ lệ giao nhận!** 🚀