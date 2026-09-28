---
title: "🚀 Theo dõi tự động sức khỏe SEO website với Google Sheets, báo cáo PDF và cảnh báo Gmail"
description: "Tự động hóa theo dõi sức khỏe SEO website hàng ngày, gửi cảnh báo khi điểm số thấp và tạo báo cáo PDF lưu trữ trên Google Drive - giải pháp hoàn toàn không cần code cho các chuyên gia SEO."
slug: "theo-doi-tu-dong-suc-khoe-seo-website"
tags: [n8n, automation, no-code, SEO, Google Sheets, Google Drive, Gmail]
keywords: [n8n workflow, tự động hóa SEO, theo dõi website, báo cáo SEO, cảnh báo tự động]
---

# 🚀 Theo dõi tự động sức khỏe SEO website với Google Sheets, báo cáo PDF và cảnh báo Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các chuyên gia SEO khi phải theo dõi thủ công hàng chục website hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 8+ giờ mỗi tuần cho việc theo dõi thủ công
- Nhận cảnh báo tức thì khi website có vấn đề SEO
- Lưu trữ lịch sử kiểm tra và báo cáo PDF chuyên nghiệp
- Tự động hóa hoàn toàn quy trình SEO monitoring
- Dữ liệu được cập nhật liên tục trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets, Drive, Gmail)
- API key từ PDF.co (miễn phí cho 100 trang/tháng)
- Danh sách website cần theo dõi trong Google Sheet
- Quyền truy cập đầy đủ cho các dịch vụ Google
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7989](https://n8n.io/workflows/7989)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Website Links"**:
   - Thiết lập credentials: `googleSheetsOAuth2Api`
   - Cấu hình tham số:
     - Spreadsheet ID: ID của Google Sheet chứa danh sách website
     - Sheet Name: Tên sheet chứa dữ liệu
     - Range: Vùng dữ liệu (ví dụ: "A2:A100")

2. **Node "Send Alert Email (Low SEO Score)"**:
   - Thiết lập credentials: `gmailOAuth2`
   - Cấu hình tham số:
     - To: Địa chỉ email nhận cảnh báo
     - Subject: Tiêu đề email cảnh báo (ví dụ: "SEO Alert: [DOMAIN]")

3. **Node "Update Performance Log"**:
   - Thiết lập credentials: `googleSheetsOAuth2Api`
   - Cấu hình tham số:
     - Spreadsheet ID: ID của Google Sheet lưu kết quả
     - Sheet Name: Tên sheet lưu dữ liệu
     - Range: Vùng dữ liệu (ví dụ: "B2:D100")

4. **Node "Save SEO Report to Drive"**:
   - Thiết lập credentials: `googleDriveOAuth2Api`
   - Cấu hình tham số:
     - Folder ID: ID thư mục lưu trữ báo cáo
     - File Name: Tên file PDF (có thể chứa biến {{DOMAIN}})

#### 3. Kích hoạt ⚡️
1. Kiểm tra workflow bằng cách chạy thử với 1-2 website mẫu
2. Sau khi xác nhận hoạt động, nhấn "Active" để kích hoạt workflow
3. Đặt lịch chạy hàng ngày lúc 9 AM thông qua node "Daily 9 AM Trigger"

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Teams để nhận cảnh báo tức thời
2. Thêm node lưu log chi tiết vào Google Sheets
3. Tạo báo cáo tổng hợp hàng tuần/ tháng từ dữ liệu thu thập
4. Kết nối với các công cụ SEO khác như Ahrefs, SEMrush để tích hợp dữ liệu

### 📌 Kết luận
Workflow này biến quy trình theo dõi SEO thủ công thành một quy trình tự động hoàn toàn, giúp các chuyên gia SEO tập trung vào phân tích và tối ưu hóa thay vì việc theo dõi. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!