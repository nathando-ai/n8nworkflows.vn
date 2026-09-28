---
title: "🚀 Tự động trích xuất dữ liệu doanh nghiệp từ Yelp bằng Bright Data và Google Sheets"
description: "Workflow n8n tự động hóa việc thu thập thông tin chi tiết doanh nghiệp từ trang Yelp và lưu vào Google Sheets, tiết kiệm thời gian và công sức cho các sếp nghiên cứu thị trường."
slug: "tu-dong-trich-xuat-du-lieu-yelp-bang-bright-data-va-google-sheets"
tags: [n8n, automation, no-code, research, market-research]
keywords: [n8n workflow, tự động hóa, trích xuất dữ liệu, Yelp, Bright Data, Google Sheets]
---

# 🚀 Tự động trích xuất dữ liệu doanh nghiệp từ Yelp bằng Bright Data và Google Sheets

[Các sếp] có bao giờ phải tự tay copy thông tin doanh nghiệp từ trang Yelp để phân tích thị trường? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhập URL đến lưu dữ liệu vào Google Sheets, tiết kiệm thời gian quý giá và giảm thiểu sai sót.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ 30 giây đến 5 phút tùy theo tốc độ mạng.
- **Chính xác cao**: Dữ liệu được trích xuất từ trang Yelp chính thức, không bị sai lệch.
- **Tích hợp dễ dàng**: Kết quả được lưu trực tiếp vào Google Sheets, thuận tiện cho phân tích.
- **Tự động hóa liên tục**: Workflow có thể chạy định kỳ để cập nhật dữ liệu mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Bright Data**: Đăng ký và lấy API key từ [Bright Data](https://brightdata.com/).
- **Google Sheets**: Tạo một Google Sheet mới và chia sẻ với tài khoản dịch vụ của bạn.
- **Tài khoản n8n**: Đã cài đặt và cấu hình n8n trên VPS hoặc máy chủ riêng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút **"Import from URL"** và nhập URL sau: [https://n8n.io/workflows/6373](https://n8n.io/workflows/6373).
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/6373) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "📥 Form Trigger"**: Không cần cấu hình gì thêm.
- **Node "🔍 Trigger Bright Data Scrape"**:
  - Chọn credentials của Bright Data.
  - Điền URL của trang Yelp vào trường `URL`.
- **Node "📡 Monitor Snapshot Status"**:
  - Chọn credentials của Bright Data.
  - Điền `snapshot_id` từ response của node trước đó.
- **Node "📊 Store to Google Sheet"**:
  - Chọn credentials của Google Sheets.
  - Điền `spreadsheetId` và `range` (ví dụ: `Yelp scraper data by URL!A1`).

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút **"Execute Workflow"** để test với dữ liệu mẫu.
2. Sau khi test thành công, nhấn vào nút **"Activate"** để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa định kỳ**: Sử dụng node "Schedule Trigger" để chạy workflow hàng ngày.
- **Thông báo kết quả**: Kết nối với Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành.
- **Xử lý lỗi**: Thêm node "Error Trigger" để xử lý các lỗi xảy ra trong quá trình chạy.
- **Lưu log**: Sử dụng node "File" để lưu log của workflow.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc thu thập dữ liệu từ Yelp, tiết kiệm thời gian và công sức. Với việc tích hợp Bright Data và Google Sheets, các sếp có thể dễ dàng phân tích và đưa ra quyết định kinh doanh chính xác hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!