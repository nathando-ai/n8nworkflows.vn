---
title: "🚀 Tự động hóa sinh lead theo mã ZIP với Google Maps và Sheets"
description: "Hướng dẫn tự động thu thập lead kinh doanh dựa trên mã ZIP, tích hợp Google Maps và Google Sheets để phân tích thị trường và quản lý dữ liệu hiệu quả."
slug: "tu-dong-hoa-sinh-lead-theo-ma-zip-voi-google-maps-va-sheets"
tags: [n8n, automation, lead generation, google maps, google sheets]
keywords: [n8n workflow, tự động hóa sinh lead, mã ZIP, Google Maps API, quản lý dữ liệu]
---

# 🚀 Tự động hóa sinh lead theo mã ZIP với Google Maps và Sheets

[Các sếp] có biết rằng việc thu thập lead kinh doanh thủ công là một công việc tốn thời gian và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ tìm kiếm lead theo mã ZIP đến lưu trữ và phân tích dữ liệu trên Google Sheets, chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ tìm kiếm lead đến lưu trữ dữ liệu.
- **Chính xác cao**: Sử dụng Google Maps API để lấy thông tin chính xác về địa điểm kinh doanh.
- **Quản lý dữ liệu hiệu quả**: Lưu trữ và phân tích dữ liệu lead trên Google Sheets.
- **Hoạt động liên tục**: Workflow có thể chạy tự động theo lịch trình hoặc theo yêu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets và Google Maps API đã kích hoạt.
- API Key của Google Maps.
- Tài khoản Telegram (nếu sử dụng node Telegram).
- Tài khoản Discord (nếu sử dụng node Discord).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11622).
2. Click vào nút "Copy Workflow to Clipboard".
3. Mở n8n Editor, click vào "Import from Clipboard".
4. Dán nội dung đã copy và click "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Get All Zip Code"**: Cấu hình Google Sheets credentials và chỉ định Sheet ID, Sheet Name chứa danh sách mã ZIP.
- **Node "Google Map API"**: Điền API Key của Google Maps vào credentials.
- **Node "Add rows in Google Sheets"**: Cấu hình Google Sheets credentials và chỉ định Sheet ID, Sheet Name để lưu trữ dữ liệu lead.
- **Node "Schedule"**: Thiết lập lịch chạy workflow theo nhu cầu (ví dụ: hàng ngày, hàng tuần).
- **Node "Limit"**: Thiết lập số lượng lead tối đa mỗi lần chạy để tránh quá tải.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để test run dữ liệu mẫu.
2. Kiểm tra kết quả trên Google Sheets để đảm bảo dữ liệu được lưu trữ đúng.
3. Bật Active workflow để chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành.
- **Lưu log hoạt động**: Thêm node để lưu log hoạt động của workflow vào Google Sheets hoặc cơ sở dữ liệu.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp lead hàng tuần qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình sinh lead theo mã ZIP, từ tìm kiếm đến lưu trữ và phân tích dữ liệu. Với việc tích hợp Google Maps và Google Sheets, các sếp có thể thu thập và quản lý dữ liệu lead một cách hiệu quả và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất kinh doanh!