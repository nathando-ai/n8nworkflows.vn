---
title: "🚀 Theo dõi xếp hạng từ khóa cấp URL trong Google Sheets với DataForSEO"
description: "Tự động hóa theo dõi xếp hạng từ khóa cấp URL trên Google bằng DataForSEO và lưu kết quả vào Google Sheets. Tiết kiệm thời gian và nâng cao hiệu quả SEO."
slug: "theo-doi-xep-hang-tu-khoa-cap-url-voi-dataforseo"
tags: [n8n, automation, no-code, seo, dataforseo, google-sheets]
keywords: [n8n workflow, tự động hóa, seo, từ khóa cấp url, dataforseo, google sheets]
---

# 🚀 Theo dõi xếp hạng từ khóa cấp URL trong Google Sheets với DataForSEO

[Các sếp SEO] đang gặp khó khăn khi phải theo dõi xếp hạng từ khóa cấp URL thủ công trên Google? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình theo dõi xếp hạng từ khóa cấp URL và lưu kết quả vào Google Sheets một cách liên tục.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình theo dõi xếp hạng từ khóa cấp URL.
- Chính xác: Lấy dữ liệu xếp hạng từ khóa cấp URL từ Google một cách chính xác và liên tục.
- Cá nhân hóa: Theo dõi xếp hạng từ khóa cấp URL cho từng URL riêng biệt.
- Hoạt động liên tục: Workflow chạy tự động theo lịch trình đã đặt, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để tạo và quản lý Google Sheets.
- Tài khoản DataForSEO để truy cập API và lấy dữ liệu xếp hạng từ khóa cấp URL.
- Google Sheets với dữ liệu đầu vào bao gồm các cột: URL, Keyword, Active (xem [ví dụ tại đây](https://docs.google.com/spreadsheets/d/1WPeLL-5futt5PzcUvbQRX3k2RXCEpliddJWuNlfdLR4/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15184](https://n8n.io/workflows/15184).
2. Click vào nút "Import" để tải xuống file JSON của workflow.
3. Trong n8n Editor, click vào menu "Workflow" > "Import from File" và chọn file JSON vừa tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Đặt lịch trình chạy workflow theo nhu cầu (mặc định là mỗi 2 tuần).

2. **Node "Create sheet"**:
   - Chọn hoặc tạo kết nối Google Sheets.
   - Chọn spreadsheet đầu ra.

3. **Node "Get live google organic SERP regular"**:
   - Chọn hoặc tạo kết nối DataForSEO.
   - Đảm bảo tài khoản DataForSEO có đủ credit để thực hiện các yêu cầu API.

4. **Node "Append or update row in sheet"**:
   - Chọn kết nối Google Sheets đã được cấu hình.
   - Chọn spreadsheet đầu ra và cấu hình các tham số cần thiết.

5. **Node "Append row in sheet"**:
   - Chọn kết nối Google Sheets đã được cấu hình.
   - Chọn spreadsheet đầu ra và cấu hình các tham số cần thiết.

6. **Node "Get keywords and URLs"**:
   - Chọn kết nối Google Sheets đã được cấu hình.
   - Chọn spreadsheet đầu vào và cấu hình các tham số cần thiết.

7. **Node "Filter (only active)"**:
   - Cấu hình bộ lọc để chỉ lấy các từ khóa hoạt động (Active = TRUE).

8. **Node "Loop over items (each keyword)"**:
   - Cấu hình số lượng từ khóa xử lý trong mỗi batch.

9. **Node "Is a new sheet created?"**:
   - Cấu hình điều kiện để kiểm tra xem sheet mới đã được tạo chưa.

10. **Node "Prepare column data for GS"**:
    - Cấu hình các cột dữ liệu cần thiết cho Google Sheets.

11. **Node "Find the row with the keyword"**:
    - Chọn kết nối Google Sheets đã được cấu hình.
    - Chọn spreadsheet đầu vào và cấu hình các tham số cần thiết.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Chạy workflow với dữ liệu mẫu để kiểm tra tính chính xác và hiệu suất.
2. **Bật Active workflow**:
   - Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, bật chế độ Active để workflow chạy tự động theo lịch trình đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm các node để gửi thông báo kết quả xếp hạng từ khóa cấp URL qua Slack hoặc Telegram.
- **Lưu log**: Thêm các node để lưu log hoạt động của workflow để theo dõi và giải quyết vấn đề nếu có.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo xếp hạng từ khóa cấp URL định kỳ qua email.
- **Tích hợp với các công cụ SEO khác**: Kết hợp với các công cụ SEO khác như Ahrefs, SEMrush để lấy dữ liệu bổ sung và phân tích sâu hơn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi xếp hạng từ khóa cấp URL trên Google và lưu kết quả vào Google Sheets một cách liên tục. Với việc tự động hóa, các sếp có thể tiết kiệm thời gian, nâng cao hiệu quả SEO và đưa ra quyết định dựa trên dữ liệu chính xác và cập nhật liên tục. Hãy áp dụng ngay workflow này để tối ưu hóa chiến lược SEO của các sếp!